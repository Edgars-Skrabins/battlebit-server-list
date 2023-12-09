<script setup lang="ts">
defineProps<{
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
}>()

</script>

<template>
  <div class="server">

    <h2> {{ Name }} </h2>

    <div class="server__map-row">

      <p> Map: <span>{{Map}}</span> </p>
      <p> Map Size: <span>{{MapSize}}</span> </p>
      <p> Gamemode: <span>{{Gamemode}}</span> </p>
      <p> Day/Night: <span>{{DayNight}}</span></p>

    </div>

    <div class="server__players-row">

      <p> Player Amount: <span>{{Players}} / {{MaxPlayers}}</span> </p>
      <p> Player's in queue: <span>{{QueuePlayers}}</span> </p>

    </div>

    <div class="server__info">

      <p> Official: <span>{{IsOfficial}}</span> </p>
      <p> Hz: <span>{{Hz}}Hz</span> </p>
      <p> Anti-cheat: <span>{{AntiCheat}}</span> </p>
      <p> Requires password: <span>{{HasPassword}}</span> </p>
      <p> Build: <span>{{Build}}</span></p>

    </div>

  </div>


</template>

<style scoped>

h2{
  font-size: 2rem;
  margin: 0.9rem 0.5rem 0.5rem 0.5rem;

  color: white;
}

p{
  font-size: 1.2rem;
  color: #b6b6b6;
}

span{
  color: #ffffff;
  font-size: 1.5rem;
  font-weight: bold;
}

.server{
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;

  background-color: rgba(33, 33, 33, 0.72);
  border-style: solid;
  border-color: #4d4c4c;

  border-radius: 2rem;
  margin: 2rem;
  padding: 1rem;

  text-align: center;

  filter: drop-shadow(0 0 1rem rgba(31, 31, 31, 0.66));
}

.server__map-row{
  display: flex;
  flex-direction: row;
  flex-wrap: nowrap;

  gap: 1.25rem;
}

.server__players-row{
  display: flex;
  flex-direction: row;
  flex-wrap: nowrap;

  gap: 1.25rem;
}

.server__info{
  display: flex;
  flex-direction: row;
  flex-wrap: nowrap;

  gap: 1.2rem;
}

</style>
