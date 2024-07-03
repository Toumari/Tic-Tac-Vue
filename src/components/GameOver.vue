<template>
    <div>
        <h1>Game Over</h1>
        <p>Winner: {{ props.winner }}</p>
        <button @click="$emit('onRestart')">Restart Game</button>
    </div>
</template>

<script setup>

import { ref } from 'vue'

const props = defineProps({
    winner: String
})

console.log(props.winner)


</script>

<style scoped>
div {
    position: absolute;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.9);
    display: flex;
    color: white;
    flex-direction: column;
    justify-content: center;
    align-items: center;
}

button {
    display: block;

}
</style>