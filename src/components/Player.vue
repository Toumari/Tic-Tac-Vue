<template>
    <div class="player">
        <h2 class="player-name">{{ name }}</h2>
        <p class="player-symbol">{{ symbol }}</p>
        <input v-if="isEditing" type="text" v-model="name">
        <button @click="handleIsEditing">{{ isEditing ? 'Save' : 'Edit' }}</button>
    </div>
</template>

<script setup>

const props = defineProps(
    {
        player: String,
        symbol: String
    }
)

import { defineProps, ref } from 'vue'

const isEditing = ref(false)

const name = ref(props.player)


const handleIsEditing = () => {
    isEditing.value = !isEditing.value
    console.log(isEditing.value)

    name.value = name.value;
}



</script>

<style scoped>
.player {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 1rem;
    background-color: #f0f0f0;
    padding: 1rem;
    border-radius: 0.5rem;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
    min-width: 150px;
}

.player-name {
    margin: 0;
}

.player-symbol {
    margin: 0;
}

input {
    width: 100%;
    padding: 0.5rem;
    border: 1px solid #ccc;
    border-radius: 0.25rem;
}

button {
    padding: 0.5rem 1rem;
    border: none;
    border-radius: 0.25rem;
    background-color: #007bff;
    color: white;
    cursor: pointer;
}

button:hover {
    background-color: #0056b3;
}

button:focus {
    outline: none;
}

button:active {
    transform: translateY(1px);
}
</style>