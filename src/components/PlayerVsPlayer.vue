<script setup lang="ts">
import { ref, provide } from "vue";
import BoardGameRow from "./TableCaro/BoardGameRow.vue"


var addBinary = function (a: string, b: string) {
  let result = [];
  let arrayA = a.split('')
  let arrayB = b.split('')
  let diff = arrayA.length - arrayB.length
  if (diff > 0) {
    for (let i = 0; i < diff; i++) {
      arrayB.unshift('0')
    }
  } else {
    for (let i = 0; i < diff; i++) {
      arrayB.unshift('0')
    }
  }
  console.log(arrayA, arrayB);
  for (let i = 0; i <= arrayA.length - 1; i++) {
    console.log(arrayA[arrayA.length - 1 - i], arrayB[arrayB.length - 1 - i]);
    if (arrayA[arrayA.length - 1 - i] + arrayB[arrayB.length - 1 - i] == 2) {
      console.log(2);
    }
  }
};

addBinary("1010", "11")
interface Emits {
  (event: "handleClickOut"): void;
}
const emit = defineEmits<Emits>();

const player = ref<boolean>(true);
const boards = ref<string[][]>([]);
const winner = ref<string>("");
const size = ref<number>(20);
const gameOver = ref<boolean>(false)
const count = ref<number[]>([1, 1, 1, 1])
// create table
for (let i = 0; i < size.value; i++) {
  boards.value[i] = [];
  for (let j = 0; j < size.value; j++) {
    boards.value[i].push("");
  }
}
provide('provideBoard', boards)


const whenWin = () => {
  winner.value = player.value ? 'O' : 'X'
  gameOver.value = !gameOver.value
}
const checkWin = (x) => {
  for (let i = 0; i < 4; i++) {
    x[i] >= 5 ? whenWin() : 0
  }

}

const resetCount = () => {
  count.value = [1, 1, 1, 1]
}
const handleClick = (indexCol, indexRow) => {
  if (boards.value[indexRow][indexCol] === "") {
    if (player.value) {
      boards.value[indexRow][indexCol] = "/src/assets/imgs/X.png";
    } else {
      boards.value[indexRow][indexCol] = "/src/assets/imgs/O.png";
    }
    player.value = !player.value;
    resetCount()
    for (let i = 1; i <= 4; i++) {

      if ((indexRow + i < size.value && boards.value[indexRow][indexCol] === boards.value[indexRow + i][indexCol])) {
        count.value[1]++;
      }
      if ((indexRow - i >= 0 && boards.value[indexRow][indexCol] === boards.value[indexRow - i][indexCol])) {
        count.value[1]++;
      }

      if (indexCol - i >= 0 && indexRow + i < size.value && boards.value[indexRow][indexCol] === boards.value[indexRow + i][indexCol - i]) {
        count.value[2]++;
      }
      if (indexRow - i >= 0 && indexCol + i >= 0 && boards.value[indexRow][indexCol] === boards.value[indexRow - i][indexCol + i]) {
        count.value[2]++
      }
      if (indexCol + i <= size.value && indexRow + i < size.value && boards.value[indexRow][indexCol] === boards.value[indexRow + i][indexCol + i]) {
        count.value[3]++
      }
      if (indexCol - i >= 0 && indexRow - i >= 0 && boards.value[indexRow][indexCol] === boards.value[indexRow - i][indexCol - i]) {
        count.value[3]++
      }
      if (boards.value[indexRow][indexCol] !== boards.value[indexRow][indexCol + i] && boards.value[indexRow][indexCol] !== boards.value[indexRow][indexCol - i]) {
      } else { count.value[0]++; }
    }
    checkWin(count.value)
    // {//   // hang doc

    // // for (let i = 1; i <= 4 && indexRow + i < size.value; i++) {
    // //   if (boards.value[indexRow][indexCol] !== boards.value[indexRow + i][indexCol]) {
    // //     break;
    // //   }
    // //   count.value++;
    // // }
    // // for (let i = 1; i <= 4 && indexRow - i >= 0; i++) {
    // //   if (boards.value[indexRow][indexCol] !== boards.value[indexRow - i][indexCol]) {
    // //     break;
    // //   }
    // //   count.value++;
    // // }
    // // ====
    // // for (let i = 1; i <= 4; i++) {
    // //   indexRow + i < size.value ? boards.value[indexRow][indexCol] !== boards.value[indexRow + i][indexCol] ? 0 : count.value++ : 0
    // //   indexRow - i >= 0 ? boards.value[indexRow][indexCol] !== boards.value[indexRow - i][indexCol] ? 0 : count.value++ : 0
    // // }
    // for (let i = 1; i <= 4; i++) {

    // }
    // /**======= */

    // // for (let i = 1; i <= 4; i++) {
    // //   if (indexRow + i < size.value && boards.value[indexRow][indexCol] !== boards.value[indexRow + i][indexCol]) {
    // //     break
    // //   }
    // //   if (indexRow - i >= 0 && boards.value[indexRow][indexCol] !== boards.value[indexRow - i][indexCol]) {
    // //     break
    // //   }


    // //   count.value++
    // // }


    // // ====
    // checkWin(count.value)
    // // duong cheo
    // resetCount()
    // for (let i = 1; i <= 4; i++) {

    // }
    // checkWin(count.value)
    // // duong cheo
    // resetCount()
    // for (let i = 1; i <= 4; i++) {

    // }

    // // 
    // // for (let i = 1; i <= 4; i++) {
    // //   indexCol + i <= size.value ? indexRow + i < size.value ? boards.value[indexRow][indexCol] === boards.value[indexRow + i][indexCol + i] ? 0 : count.value++ : 0 : 0
    // //   indexCol - i >= 0 ? indexRow - i >= 0 ? boards.value[indexRow][indexCol] ===
    // //     boards.value[indexRow - i][indexCol - i] ? 0 : count.value++ : 0 : 0
    // // }
    // // 
    // }
  }
};
const resetAll = () => {
  for (let i = 0; i < size.value; i++) {
    boards.value[i] = new Array();
    for (let j = 0; j < size.value; j++) {
      boards.value[i].push("");
    }
  }

  gameOver.value = false
}
const handleClickOut = () => {
  resetAll()
  emit('handleClickOut')
}

</script>
<template>
  <div class="flex gap-5 relative">
    <div class="absolute -left-32 top-2/4 -translate-y-1/2 flex flex-col">
      <button @click="handleClickOut" class="bg-[#F4F5FA] px-4 py-3 rounded-full border border-[#F0F0F6] shadow-xl mt-4">
        Quit
      </button><button @click="resetAll"
        class="bg-[#F4F5FA] px-4 py-3 rounded-full border border-[#F0F0F6] shadow-xl mt-4">
        Play again
      </button>
    </div>
    <div :class="{ 'pointer-events-none': gameOver }">
      <board-game-row v-for="(row, index) in boards" :key="index" :row="row" :indexRow="index" :boards="boards"
        @handle-click="handleClick"></board-game-row>
    </div>
  </div>
  <div class="bg-[#B3C890]  rounded-lg z-10 absolute top-1/2 left-1/2 -translate-y-1/2 -translate-x-1/2 bg-opacity-90"
    :class="{ 'hidden': !gameOver }">
    <div class="p-10 rounded-xl">
      <!-- headers content-->
      <div class="flex flex-col justify-center items-center text-center">
        <h1 class="max-w-sm font-bold font-sans  w-screen">{{ winner }} Win </h1>
      </div>
    </div>
  </div>
</template>
<style></style>
