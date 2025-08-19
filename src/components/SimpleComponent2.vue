<script setup>
import { defineProps } from 'vue'

const props = defineProps(["todoItems"]);
// const props = defineProps({
//     todoItems: {
//         type: Array
//     }
// });
</script>

<template>
    <ol>
        <li v-for="todoItem in todoItems">{{ todoItem }}</li>
    </ol>
</template>