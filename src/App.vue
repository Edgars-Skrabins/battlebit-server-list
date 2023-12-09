<script setup lang="ts">
import {ref, onMounted} from 'vue';
import axios from 'axios';
import ServerCard from './components/ServerCard.vue';

type GameServer = {
  Name: string;
  Map: string;
  MapSize: string;
  Gamemode: string;
  Region: string;
  Players: number;
  QueuePlayers: number;
  MaxPlayers: number;
  Hz: number;
  DayNight: string;
  IsOfficial: boolean;
  HasPassword: boolean;
  AntiCheat: string;
  Build: string;
};

const apiUrl = 'https://publicapi.battlebit.cloud/Servers/GetServerList';
let gameServers = ref<GameServer[]>([]);

onMounted(async () => {
  try {
    const response = await axios.get(apiUrl);
    gameServers.value = response.data;
    console.log('Successfully received data ', gameServers.value);
  } catch (error) {
    console.log('Failed to receive data ', error);
  }
});


let sortByPlayersBackwards = false;
const sortByPlayers = () => {
  if (sortByPlayersBackwards) {
    gameServers.value = gameServers.value.sort((a, b) => a.Players - b.Players);
    sortByPlayersBackwards = false;
  } else {
    gameServers.value = gameServers.value.sort((a, b) => b.Players - a.Players);
    sortByPlayersBackwards = true;
  }
}

let sortByHzBackwards = false;
const sortByHz = () => {
  if (sortByHzBackwards) {
    gameServers.value = gameServers.value.sort((a, b) => a.Hz - b.Hz);
    sortByHzBackwards = false;
  } else {
    gameServers.value = gameServers.value.sort((a, b) => b.Hz - a.Hz);
    sortByHzBackwards = true;
  }
}

const getMapSizeValue = (mapSize: string): number => {
  switch (mapSize) {
    case "Ultra":
      return 5;
    case "Big":
        return 4;
    case "Medium":
        return 3;
    case "Tiny":
        return 2;
    default:
      return 0;
  }
};


let sortByMapSizeBackwards = false;
const sortByMapSize = () => {
  if (sortByMapSizeBackwards) {
    gameServers.value = gameServers.value.sort((a, b) => getMapSizeValue(a.MapSize) - getMapSizeValue(b.MapSize));
    sortByMapSizeBackwards = false;
  } else {
    gameServers.value = gameServers.value.sort((a, b) => getMapSizeValue(b.MapSize) - getMapSizeValue(a.MapSize));
    sortByMapSizeBackwards = true;
  }
}

</script>

<template>
  <div class="container">
    <h1> Battlebit Servers </h1>
    <div class="buttons">
      <button @click="sortByHz"> Hz</button>
      <button @click="sortByPlayers"> Players</button>
      <button @click="sortByMapSize"> Map Size</button>

    </div>

    <div>
      <div class="servers" v-for="(server, index) in gameServers" :key="index">
        <ServerCard
            :Name="server.Name"
            :Map="server.Map"
            :MapSize="server.MapSize"
            :Gamemode="server.Gamemode"
            :Region="server.Region"
            :Players="server.Players"
            :QueuePlayers="server.QueuePlayers"
            :MaxPlayers="server.MaxPlayers"
            :Hz="server.Hz"
            :DayNight="server.DayNight"
            :IsOfficial="server.IsOfficial"
            :HasPassword="server.HasPassword"
            :AntiCheat="server.AntiCheat"
            :Build="server.Build"
        />
      </div>
    </div>
  </div>
</template>

<style scoped>


h1 {
  color: white;
  font-size: 3rem;
  font-weight: bolder;
}

.container {
  font-weight: bolder;

  font-family: "Microsoft PhagsPa";
  background: linear-gradient(to bottom, #1a1a1a, #101010);

  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;

  margin: 0;
  padding: 0;

}

button {
  font-size: 1.7rem;
  border-radius: 0.4rem;
  border-style: solid;
  border-width: 0.14rem;
  border-color: #4d4c4c;

  color: white;

  padding: 0.5rem 1rem;
  background-color: rgba(47, 47, 47, 0.37);

  transition: 0.08s;

  &:hover {
    cursor: pointer;
    border-color: #7a7979;
    background-color: rgba(47, 47, 47, 0.58);
  }
}

.buttons {
  display: flex;
  flex-direction: row;

  gap: 4rem;
}

</style>
