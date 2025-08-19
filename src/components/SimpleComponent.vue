<script setup>
import { ref } from 'vue';
import SimpleComponent2 from '../components/SimpleComponent2.vue';

const todoItems = ref([
    "Vegetables",
    "Cheese",
    "Whatever else humans are supposed to eat"
]);
</script>

<template>
    <div class="wrapper">
        <SimpleComponent2 :todo-items="todoItems" />
    </div>
</template>