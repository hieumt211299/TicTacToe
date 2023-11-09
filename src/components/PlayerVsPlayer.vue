<script setup lang="ts">
import { ref, provide } from "vue";
import BoardGameRow from "./TableCaro/BoardGameRow.vue";

interface Emits {
  (event: "handleClickOut"): void;
}
interface location {
  preRow: number;
  preCol: number;
  item: string;
}

const emit = defineEmits<Emits>();

const player = ref<boolean>(true);
const boards = ref<string[][]>([]);
const winner = ref<string>("");
const size = ref<number>(20);
const gameOver = ref<boolean>(false);
const count = ref<number[]>([1, 1, 1, 1]);
const previousMove = ref<location[]>([]);
// create table
for (let i = 0; i < size.value; i++) {
  boards.value[i] = [];
  for (let j = 0; j < size.value; j++) {
    boards.value[i].push("");
  }
}
provide("provideBoard", boards);

const whenWin = () => {
  winner.value = player.value ? "O" : "X";
  gameOver.value = !gameOver.value;
};
const checkWin = (x) => {
  for (let i = 0; i < 4; i++) {
    x[i] >= 5 ? whenWin() : 0;
  }
};

const resetCount = () => {
  count.value = [1, 1, 1, 1];
};
const handleClick = (indexCol, indexRow) => {
  if (boards.value[indexRow][indexCol] === "") {
    if (player.value) {
      boards.value[indexRow][indexCol] =
        "data:image/png;base64,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";
    } else {
      boards.value[indexRow][indexCol] =
        "https://cdn-icons-png.flaticon.com/512/4553/4553010.png";
    }
    player.value = !player.value;
    previousMove.value = [
      {
        preRow: indexRow,
        preCol: indexCol,
        item: boards.value[indexRow][indexCol],
      },
    ];
    resetCount();
    for (let i = 1; i <= 4; i++) {
      if (
        indexRow + i < size.value &&
        boards.value[indexRow][indexCol] ===
          boards.value[indexRow + i][indexCol]
      ) {
        count.value[1]++;
      }
      if (
        indexRow - i >= 0 &&
        boards.value[indexRow][indexCol] ===
          boards.value[indexRow - i][indexCol]
      ) {
        count.value[1]++;
      }

      if (
        indexCol - i >= 0 &&
        indexRow + i < size.value &&
        boards.value[indexRow][indexCol] ===
          boards.value[indexRow + i][indexCol - i]
      ) {
        count.value[2]++;
      }
      if (
        indexRow - i >= 0 &&
        indexCol + i >= 0 &&
        boards.value[indexRow][indexCol] ===
          boards.value[indexRow - i][indexCol + i]
      ) {
        count.value[2]++;
      }
      if (
        indexCol + i <= size.value &&
        indexRow + i < size.value &&
        boards.value[indexRow][indexCol] ===
          boards.value[indexRow + i][indexCol + i]
      ) {
        count.value[3]++;
      }
      if (
        indexCol - i >= 0 &&
        indexRow - i >= 0 &&
        boards.value[indexRow][indexCol] ===
          boards.value[indexRow - i][indexCol - i]
      ) {
        count.value[3]++;
      }
      if (
        boards.value[indexRow][indexCol] !==
          boards.value[indexRow][indexCol + i] &&
        boards.value[indexRow][indexCol] !==
          boards.value[indexRow][indexCol - i]
      ) {
      } else {
        count.value[0]++;
      }
    }
    checkWin(count.value);
  }
};
const resetAll = () => {
  for (let i = 0; i < size.value; i++) {
    boards.value[i] = new Array();
    for (let j = 0; j < size.value; j++) {
      boards.value[i].push("");
    }
  }

  gameOver.value = false;
};
const handleClickOut = () => {
  resetAll();
  emit("handleClickOut");
};
const undo = () => {
  if (previousMove.value.length) {
    boards.value[previousMove.value[0].preRow][previousMove.value[0].preCol] =
      "";
    player.value = !player.value;
  }
  previousMove.value = [];
};
</script>
<template>
  <div class="flex gap-5 relative">
    <div class="absolute -left-32 top-2/4 -translate-y-1/2 flex flex-col">
      <button
        @click="handleClickOut"
        class="bg-[#F4F5FA] px-4 py-3 rounded-full border border-[#F0F0F6] shadow-xl mt-4"
      >
        Quit
      </button>
      <button
        @click="resetAll"
        class="bg-[#F4F5FA] px-4 py-3 rounded-full border border-[#F0F0F6] shadow-xl mt-4"
      >
        Play again
      </button>
      <button
        @click="undo"
        class="bg-[#F4F5FA] px-4 py-3 rounded-full border border-[#F0F0F6] shadow-xl mt-4"
        :class="{ 'pointer-events-none': gameOver }"
      >
        undo
      </button>
    </div>
    <div :class="{ 'pointer-events-none': gameOver }">
      <board-game-row
        v-for="(row, index) in boards"
        :key="index"
        :row="row"
        :indexRow="index"
        :boards="boards"
        @handle-click="handleClick"
      ></board-game-row>
    </div>
  </div>
  <div
    class="bg-[#B3C890] rounded-lg z-10 absolute top-1/2 left-1/2 -translate-y-1/2 -translate-x-1/2 bg-opacity-90"
    :class="{ hidden: !gameOver }"
  >
    <div class="p-10 rounded-xl">
      <!-- headers content-->
      <div class="flex flex-col justify-center items-center text-center">
        <h1 class="max-w-sm font-bold font-sans w-screen">{{ winner }} Win</h1>
      </div>
    </div>
  </div>
</template>
<style></style>
