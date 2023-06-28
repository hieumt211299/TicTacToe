<script setup>
import HelloWorld from "./components/HelloWorld.vue";
import PlayerVsPlayer from "./components/PlayerVsPlayer.vue";
</script>

<template>
  <HelloWorld
    class="bg-[#C2CAD0] min-h-fit p-28 rounded-3xl"
    msg="Vite + Vue"
  />
  <div class="hidden">
    <PlayerVsPlayer></PlayerVsPlayer>
  </div>
</template>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}

.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
