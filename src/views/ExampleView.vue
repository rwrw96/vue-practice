<script setup lang="ts">
import { ref } from 'vue';
import HandingUserInput from '../components/HandlingUserInput.vue';

const isHideHandingUserInput = ref(false)

function toggleHideHandingUserInput() {
    isHideHandingUserInput.value = !isHideHandingUserInput.value
}
</script>

<template>
    <HandingUserInput v-if="isHideHandingUserInput"/>
    <div class="hide-button-wrapper">
        <button class="" @click="toggleHideHandingUserInput()">HandingUserInput</button>
    </div>
</template>

<style>

</style>