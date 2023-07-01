<script setup lang="ts">
import { inject, Ref } from "vue";

// const injectBoards = inject<string[][]>('provideBoard')
// const board = ref<string[][]>(injectBoards || [])
const injectBoards = inject<Ref<string[][]>>("provideBoard") || [];

interface Props {
  col: string;
  indexCol: number;
  indexRow: number;
}
const props = defineProps<Props>();

interface Emits {
  (event: "handleClick", col: number): void;
}
const emit = defineEmits<Emits>();

const handleClick = () => {
  emit("handleClick", props.indexCol);
};
</script>
<template>
  <div
    class="w-8 h-8 flex items-center justify-center border border-collapse border-gray-700 cursor-pointer bg-gray-200"
    @click="handleClick"
  >
    <img :src="injectBoards[props.indexRow][props.indexCol]" class="p-1" />
  </div>
</template>
<style></style>
