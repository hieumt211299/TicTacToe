<script setup lang="ts">
import { ref, inject } from 'vue'
interface Props {
    col: string,
    indexCol:number,
    boards:{},
    indexRow:number
}
const props = defineProps<Props>();

interface Emits {
    (event:"handleClick",col:number):void
}
const emit=defineEmits<Emits>()

const handleClick=()=>{
    emit('handleClick',props.indexCol)
}


const symbol=ref<string>('')
if(props.boards[props.indexRow][props.indexCol]===1){
    symbol.value='X'
}
if(props.boards[props.indexRow][props.indexCol] === 2) {
    symbol.value = '0'
}



</script>
<template>
    <div class="w-8 h-8  flex items-center justify-center border border-collapse border-gray-700 cursor-pointer" @click="handleClick">
        {{ boards[props.indexRow][props.indexCol] }}
    </div >
</template>
<style></style>