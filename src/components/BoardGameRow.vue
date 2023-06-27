<script setup lang="ts">
import BoardGameCol from "./BoardGameCol.vue";

interface Props {
  row: string[];
  indexRow: number;
  boards: {};
}

const props = defineProps<Props>();
interface Emits {
  (event: "handleClick", indexCol: number, indexRow: number): void;
}
const emit = defineEmits<Emits>();

const handleClick = (indexCol) => {
  emit("handleClick", indexCol, props.indexRow);
};
</script>
<template>
  <div class="flex border-collapse">
    <BoardGameCol
      v-for="(col, index) in props.row"
      :key="index"
      :col="col"
      :indexCol="index"
      :indexRow="indexRow"
      :boards="boards"
      @handle-click="handleClick"
    ></BoardGameCol>
  </div>
</template>
<style></style>
