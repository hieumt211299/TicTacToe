<script setup lang="ts">
import { ref} from 'vue'

// =====
defineProps({
    msg: String,
})

const handle1vs1 = () => {
    console.log('1 vs 1');
}
const handle1vsbot = () => {
    console.log('1vs bot');
}
const handlebotvsbot = () => {
    console.log('bot vs bot');
}
</script>

<template>
    <!-- <h1 class="text-3xl font-bold underline">{{ msg }}</h1> -->
    <!--  -->
    <div class="flex items-center justify-center flex-col bg-[#E5E5E5] min-h-screen rounded-lg   ">
        <!-- main card -->
        <div class="p-10 rounded-xl">
            <!-- headers content-->
            <div class="flex flex-col justify-center items-center text-center">
                <h1 class="max-w-sm font-bold font-sans">
                    Tic Tac Toe
                </h1>
                <!-- <div class="font-light max-w-lg mt-5 text-sm">
                      All devices come with free delivery or pickup as standard. See information on available shopping
                      options for your location.
                  </div> -->
            </div>

            <!-- selecet mode -->
            <div class="grid grid-cols-1 gap-10 md:grid-cols-3 mt-10">
                <div class="bg-[#FFFBEC] rounded-xl ">
                    <div class="flex flex-col p-8 rounded-xl bg-white shadow-xl translate-x-4 translate-y-4 w-96 md:w-auto">
                        <div class="flex items-center justify-evenly">
                            <img src="../assets/imgs/gamer.png" class="w-8">
                            <img src="../assets/imgs/vs.png" class="w-8">
                            <img src="../assets/imgs/gamer.png" class="w-8">
                        </div>
                        <div class="mt-3 font-semibold text-lg">Player VS Player</div>
                        <!-- <div class="text-sm font-light">Up to 100Mbit/s</div> -->
                        <!-- <div class="my-4">
                              <span class="font-bold text-base">299,-</span>
                              <span class="font-light text-sm">/month</span>
                          </div> -->

                        <button class="bg-[#F4F5FA] px-4 py-3 rounded-full  border border-[#F0F0F6] shadow-xl mt-4"
                            @click="handle1vs1">
                            <a href="../components/PlayerVsPlayer.vue">Play</a>
                        </button>
                    </div>
                </div>

                <div class="bg-[#FFFBEC] rounded-xl">
                    <div class="flex flex-col p-8 rounded-xl bg-white shadow-xl translate-x-4 translate-y-4 w-96 md:w-auto">
                        <div class="flex items-center justify-evenly">
                            <img src="../assets/imgs/gamer.png" class="w-8">
                            <img src="../assets/imgs/vs.png" class="w-8">
                            <img src="../assets/imgs/bot.png" class="w-8">
                        </div>
                        <div class="mt-3 font-semibold text-lg">Player VS Bot</div>
                        <!-- <div class="text-sm font-light">Up to 100Mbit/s</div> -->
                        <!-- <div class="my-4">
                              <span class="font-bold text-base">299,-</span>
                              <span class="font-light text-sm">/month</span>
                          </div> -->

                        <button class="bg-[#F4F5FA] px-4 py-3 rounded-full  border border-[#F0F0F6] shadow-xl mt-4"
                            @click="handle1vsbot">
                            Play
                        </button>
                    </div>
                </div>


                <div class="bg-[#FFFBEC] rounded-xl">
                    <div class="flex flex-col p-8 rounded-xl bg-white shadow-xl translate-x-4 translate-y-4 w-96 md:w-auto">
                        <div class="flex items-center justify-evenly">
                            <img src="../assets/imgs/bot.png" class="w-8">
                            <img src="../assets/imgs/vs.png" class="w-8">
                            <img src="../assets/imgs/bot.png" class="w-8">
                        </div>
                        <div class="mt-3 font-semibold text-lg">Bot VS Bot</div>
                        <!-- <div class="text-sm font-light">Up to 100Mbit/s</div> -->
                        <!-- <div class="my-4">
                              <span class="font-bold text-base">299,-</span>
                              <span class="font-light text-sm">/month</span>
                          </div> -->

                        <button class="bg-[#F4F5FA] px-4 py-3 rounded-full  border border-[#F0F0F6] shadow-xl mt-4"
                            @click="handlebotvsbot">
                            Play
                        </button>
                    </div>
                </div>
            </div>
            <!-- <div class="flex justify-center">
                  <button class="mt-12 bg-slate-900 text-white px-4 rounded-full py-3">See all subscriptions</button>
              </div> -->
        </div>
    </div>
</template>

<style scoped>
.read-the-docs {
    color: #888;
}
</style>

