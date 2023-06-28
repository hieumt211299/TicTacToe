<script setup lang="ts">
import { ref, inject } from "vue";

const test3 = inject('test1')
const board = ref<{}>(test3 ? test3 : {})
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
  <div class="w-8 h-8 flex items-center justify-center border border-collapse border-gray-700 cursor-pointer bg-gray-200"
    @click="handleClick">
    {{ board[props.indexRow][props.indexCol] }}
  </div>
</template>
<style></style>
