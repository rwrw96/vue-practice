<script setup lang="ts">
import { ref } from 'vue';

const titleText = ref('titleだよ')
const isRed = ref(true)
const color = ref('green')
function toggleColor() {
    color.value = color.value === 'blue' ? 'green' : 'blue'
}
</script>

<template>
    <div class="wrapper">
        <p :title="titleText">Hover your mouse over me for a few seconds to see my dynamically bound title!</p>
        <p :class="{ 'red-content' : isRed }" @click="isRed = !isRed">This should be red... but click me to toggle it.</p>
        <p :style="{ color }" @click="toggleColor">This should be green, and should toggle between green and blue on click.</p>
    </div>
</template>

<style>
.red-content {
    color: red;
}
.green-content {
    color: green;
}
.blue-content {
    color: blue;
}
</style>