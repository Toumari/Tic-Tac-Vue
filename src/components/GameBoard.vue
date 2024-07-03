<template>
    <div class="game-board">
        <div v-for="(row, rowIndex) in props.board" :key="rowIndex" class="row">
            <div v-for="(cell, cellIndex) in row" :key="cellIndex" @click="$emit('onCellClick', rowIndex, cellIndex)"
                class="cell">
                {{ cell }}
            </div>
        </div>
    </div>
</template>

<script setup>

import { ref } from 'vue'
const props = defineProps({
    board: Array,
    symbol: String
})
</script>

<style scoped>
.game-board {
    margin-top: 5rem;
    display: flex;
    flex-direction: column;
    gap: 1rem;
    align-items: center;
}

.row {
    display: flex;
    gap: 1rem;
}

.cell {
    width: 100px;
    height: 100px;
    background-color: #f0f0f0;
    border-radius: 0.5rem;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.5);
    DISPLAY: flex;
    justify-content: center;
    align-items: center;
    font-size: 2rem;
}

.cell:hover {
    cursor: pointer;
}
</style>