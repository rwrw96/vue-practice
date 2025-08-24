<script setup>
import { ref, onMounted, computed } from "vue"

const progress = ref(0)
const speed = ref(1000)
const displaySpeed = computed(() => {
    return `${speed.value/1000}s`
})

onMounted(() => {
    setInterval(() => {
        if (progress.value < 100) {
            progress.value += 1
        } else {
            clearInterval()
        }
    }, speed.value/10)
});


</script>

<template>
    <div class="progress-container">
        <progress :value="progress" :max="100"></progress>
        <p>{{ progress }}%</p>
        <input type="range" v-model="speed" min="0" max="3000">
        {{ displaySpeed }}
        <button @click="progress=0">reset</button>
    </div>
</template>

<style scoped>
.progress-container {
    width: 300px;
}

.bar {
    width: 100%;
    height: 20px;
    background: #eee;
    margin-top: 10px;
    border-radius: 10px;
    overflow: hidden;
}
.fill {
    height: 100%;
    background: #4caf50;
    transition: width 0.5s linear;
}
</style>
