<script setup lang="ts">
import { ref, provide } from "vue";
import BoardGameRow from "./BoardGameRow.vue";

interface Emits {
  (event: "handleClickOut"): void;
}
const emit = defineEmits<Emits>();
const player1 = ref<boolean>(true);
const boards = ref<{}>([]);
const winner = ref<string>("");
const size = ref<number>(20);
const gameOver =ref<boolean>(false)


// create table
for (let i = 0; i < size.value; i++) {
  boards.value[i] = new Array();
  for (let j = 0; j < size.value; j++) {
    boards.value[i].push("");
  }
}
function location(row: number, col: number) {
  return boards.value[row][col];
}
const whenWin=()=>{
  winner.value=player1.value? 'O':'X'
  gameOver.value=!gameOver.value
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

  // hang ngang
  for (let i = 1; i <= 4; i++) {
    if (
      boards.value[indexRow][indexCol] === boards.value[indexRow][indexCol + i]
    ) {
      if (
        i == 4 &&
        boards.value[indexRow][indexCol] ===
          boards.value[indexRow][indexCol + i]
      ) {
        whenWin()
      }
    } else {
      for (let j = 1; j <= 4; j++) {
        if (indexCol + i - 1 >= 0 && indexCol + i - 1 - j >= 0) {
          if (
            boards.value[indexRow][indexCol + i - 1] ===
            boards.value[indexRow][indexCol + i - 1 - j]
          ) {
            if (j == 4) {
              if (
                boards.value[indexRow][indexCol + i - 1] ===
                boards.value[indexRow][indexCol + i - 1 - j]
              ) {
                whenWin()
              }
            }
          } else {
            break;
          }
        }
      }
      break;
    }
  }
  //   // hang doc
  for (let i = 1; i <= 4; i++) {
    if (indexRow + i < size.value) {
      if (
        boards.value[indexRow][indexCol] ===
        boards.value[indexRow + i][indexCol]
      ) {
        if (i == 4) {
          if (
            boards.value[indexRow][indexCol] ===
            boards.value[indexRow + i][indexCol]
          ) {
            whenWin()
          }
        }
      } else {
        for (let j = 1; j <= 4; j++) {
          if (indexRow + i - 1 >= 0 && indexRow + i - 1 - j >= 0) {
            if (
              boards.value[indexRow + i - 1][indexCol] ===
              boards.value[indexRow + i - 1 - j][indexCol]
            ) {
              if (j == 4) {
                if (
                  boards.value[indexRow + i - 1][indexCol] ===
                  boards.value[indexRow + i - 1 - j][indexCol]
                ) {
                  whenWin()
                }
              }
            } else {
              break;
            } 
          }
        }
        break;
      }
    }
  }
  //   // duong cheo
  for (let i = 1; i <= 4; i++) {
    if (indexCol - i >= 0 && indexRow + i < size.value) {
      if (
        boards.value[indexRow][indexCol] ===
        boards.value[indexRow + i][indexCol - i]
      ) {
        if (i == 4) {
          if (
            boards.value[indexRow][indexCol] ===
            boards.value[indexRow + i][indexCol - i]
          ) {
            whenWin()
          }
        }
      } else {
        for (let j = 1; j <= 4; j++) {
          if (
            indexRow + i - 1 >= 0 &&
            indexCol - i + 1 >= 0 &&
            indexRow + i - 1 - j >= 0 &&
            indexCol - i + 1 + j >= 0
          ) {
            if (
              boards.value[indexRow + i - 1][indexCol - i + 1] ==
              boards.value[indexRow + i - 1 - j][indexCol - i + 1 + j]
            ) {
              if (j == 4) {
                if (
                  boards.value[indexRow + i - 1][indexCol - i + 1] ==
                  boards.value[indexRow + i - 1 - j][indexCol - i + 1 + j]
                ) {
                  whenWin()
                }
              }
            } else {
              break;
            }
          }
        }
        break;
      }
    }
  }

  for (let i = 1; i <= 4; i++) {
    if (indexCol + i <= size.value && indexRow + i < size.value) {
      if (
        boards.value[indexRow][indexCol] ===
        boards.value[indexRow + i][indexCol + i]
      ) {
        if (i == 4) {
          if (
            boards.value[indexRow][indexCol] ===
            boards.value[indexRow + i][indexCol + i]
          ) {
            whenWin()
          }
        }
      } else {
        for (let j = 1; j <= 4; j++) {
          if (
            indexRow + i - 1 - j >= 0 &&
            indexRow + i - 1 - j < size.value &&
            indexCol + i - 1 - j >= 0 &&
            indexCol + i - 1 - j < size.value
          ) {
            if (
              boards.value[indexRow + i - 1][indexCol + i - 1] ==
              boards.value[indexRow + i - 1 - j][indexCol + i - 1 - j]
            ) {
              if (j == 4) {
                if (
                  boards.value[indexRow + i - 1][indexCol + i - 1] ==
                  boards.value[indexRow + i - 1 - j][indexCol + i - 1 - j]
                ) {
                  whenWin()
                }
              }
            } else {
              break;
            }
          }
        }
        break;
      }
    }
  }
};
const resetAll=()=>{
    for (let i = 0; i < size.value; i++) {
  boards.value[i] = new Array();
  for (let j = 0; j < size.value; j++) {
    boards.value[i].push("");
  }
  gameOver.value=false

}
}
const handleClickOut=()=>{
  resetAll()
  emit('handleClickOut')
}
</script>
<template>
  <div class="flex gap-5 relative">
    <div class="absolute -left-32 top-2/4 -translate-y-1/2 flex flex-col" >
      <button @click="handleClickOut" class="bg-[#F4F5FA] px-4 py-3 rounded-full border border-[#F0F0F6] shadow-xl mt-4">
        Quit
      </button><button @click="resetAll" class="bg-[#F4F5FA] px-4 py-3 rounded-full border border-[#F0F0F6] shadow-xl mt-4">
        Play again
      </button>
    </div>
    <div :class=" {'pointer-events-none':gameOver}">
      <BoardGameRow
      v-for="(row, index) in boards"
      :key="index"
      :row="row"
      :indexRow="index"
      :boards="boards"
      @handle-click="handleClick"
    ></BoardGameRow>
    </div>

  </div>
  <div class="bg-[#B3C890]  rounded-lg z-10 absolute top-1/2 left-1/2 -translate-y-1/2 -translate-x-1/2 bg-opacity-90" :class="{'hidden': !gameOver}">
    <div class="p-10 rounded-xl">
      <!-- headers content-->
      <div class="flex flex-col justify-center items-center text-center">
        <h1 class="max-w-sm font-bold font-sans  w-screen">{{ winner }} Win </h1>
      </div>
    </div>
  </div>
</template>
<style></style>
