<script setup lang="ts">
import { ref, inject } from "vue";
interface Props {
  col: string;
  indexCol: number;
  boards: {};
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
    {{ boards[props.indexRow][props.indexCol] }}
  </div>
</template>
<style></style>
