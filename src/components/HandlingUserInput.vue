<script setup lang="ts">
import { ref } from 'vue';

const helloWorld = ref('Hello World!')

function reverceWord() {
    helloWorld.value = helloWorld.value.split('').reverse().join('');
}
function append() {
    helloWorld.value = helloWorld.value + "!"
}
function alertLink() {
    alert('阻止しました')
}
</script>

<template>
    <div class="wrapper">
        <h1>{{ helloWorld }}</h1>
        <button @click="reverceWord">reverce message</button>
        <button @click="append">append "!"</button>

        <a href="https://google.com" @click.prevent="alertLink">リンク</a>
    </div>
</template>

<style>
    .wrapper {
        display: flex;
        flex-direction: column;
        button {
            width: 30%;
            margin: 5px 0;
            padding: 5px;
        }
    }
</style>