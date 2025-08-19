<script setup lang="ts">
import { ref, computed } from 'vue';

const celsius = ref(0)
const fahrenheit = computed({
    get: () => celsius.value*1.8+32,
    set: (val) => celsius.value = (val-32)/1.8
})
</script>

<template>
    <div class="wraper">
        <input type="number" v-model="celsius" />
        Celsius =
        <input type="number" v-model=fahrenheit />Fahrenheit
    </div>
</template>