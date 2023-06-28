<script setup lang="ts">
import { ref, provide } from "vue";
import BoardGameRow from "./BoardGameRow.vue";

interface Emits {
  (event: "handleClick"): void;
}
const emit = defineEmits<Emits>();
const player1 = ref<boolean>(true);
const boards = ref<{}>([]);
const winner = ref<string>("");
// let data = "";
// let size= ref<number>(3)
const size=ref<number>(20)
for (let i = 0; i < size.value; i++) {
    // boards.value[i] = new Array('', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '');
    boards.value[i]=new Array()
    for(let j=0;j<size.value;j++){
        boards.value[i].push('')
    }
}

const handleClick = (indexCol, indexRow) => {
  if (boards.value[indexRow][indexCol] === "") {
    if (player1.value) {
      boards.value[indexRow][indexCol] = "X";
    } else {
      boards.value[indexRow][indexCol] = "O";
    }
    player1.value = !player1.value;
  }
  console.log(indexRow, indexCol);
  // hang ngang
  for (let i = 1; i <= 4; i++) {
    if (
      boards.value[indexRow][indexCol] === boards.value[indexRow][indexCol + i]
    ) {
      if (i == 4) {
        if (
          boards.value[indexRow][indexCol] ===
          boards.value[indexRow][indexCol + i]
        ) {
          console.log("win");
        }
      }
    } else {
      for (let j = 1; j <= 4; j++) {
        if (
          boards.value[indexRow][indexCol + i - 1] ===
          boards.value[indexRow][indexCol + i - 1 - j]
        ) {
          if (j == 4) {
            if (
              boards.value[indexRow][indexCol + i - 1] ===
              boards.value[indexRow][indexCol + i - 1 - j]
            ) {
              console.log("win");
            }
          }
        } else {
          break;
        }
      }
    }
  }
  // hang doc
  for (let i = 1; i <= 4; i++) {
    if (
      boards.value[indexRow][indexCol] === boards.value[indexRow + i][indexCol]
    ) {
      if (i == 4) {
        if (
          boards.value[indexRow][indexCol] ===
          boards.value[indexRow + i][indexCol]
        ) {
          console.log("win");
        }
      }
    } else {
      for (let j = 1; j <= 4; j++) {
        if (
          boards.value[indexRow + i - 1][indexCol] ===
          boards.value[indexRow + i - 1 - j][indexCol]
        ) {
          if (j == 4) {
            if (
              boards.value[indexRow + i - 1][indexCol] ===
              boards.value[indexRow + i - 1 - j][indexCol]
            ) {
              console.log("win");
            }
          }
        } else {
          break;
        }
      }
    }
  }
  // duong cheo
  for (let i = 1; i <= 4; i++) {
    if (
      boards.value[indexRow][indexCol] ==
      boards.value[indexRow + i][indexCol - i]
    ) {
      if (i == 4) {
        if (
          boards.value[indexRow][indexCol] ==
          boards.value[indexRow + i][indexCol - i]
        ) {
          console.log("win");
        }
      }
    } else {
      for (let j = 1; j <= 4; j++) {
        if (
          boards.value[indexRow + i - 1][indexCol - i + 1] ==
          boards.value[indexRow + i - 1 - j][indexCol - i + 1 + j]
        ) {
          if (j == 4) {
            if (
              boards.value[indexRow + i - 1][indexCol - i + 1] ==
              boards.value[indexRow + i - 1 - j][indexCol - i + 1 + j]
            ) {
              console.log("win");
            }
          }
        } else {
          break;
        }
      }
    }
  }
};
</script>
<template>
  <div class="overflow-hidden">
    <BoardGameRow
      v-for="(row, index) in boards"
      :key="index"
      :row="row"
      :indexRow="index"
      :boards="boards"
      @handle-click="handleClick"
    ></BoardGameRow>
  </div>
</template>
<style></style>
