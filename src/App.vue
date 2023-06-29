<script setup lang="ts">
import HelloWorld from "./components/HelloWorld.vue";
import PlayerVsPlayer from "./components/PlayerVsPlayer.vue";
import { ref, unref } from "vue";

const activePVP = ref<boolean>(false)
const activeMain = ref<boolean>(true)
const handleClickPVP = () => {
  activePVP.value = !unref(activePVP);
  activeMain.value = !unref(activeMain)
}
const handleClickOut = () => {
  activePVP.value = !unref(activePVP);
  activeMain.value = !unref(activeMain)
}
</script>

<template>
  <div>
    <hello-world class="min-h-fit rounded-3xl" :class="{ 'hidden': !activeMain }"
      @handle-click-p-v-p="handleClickPVP"></hello-world>
  </div>
  <div :class="{ 'hidden': !activePVP }" class="2">
    <player-vs-player @handle-click-out="handleClickOut"></player-vs-player>
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
