<script setup lang="ts">
import { ref } from 'vue';
import HandingUserInput from '../components/HandlingUserInput.vue';
import AttributeBindings from '../components/AttributeBindings.vue';

const isHideHandingUserInput = ref(false)
const isAttributeBindings = ref(false)

function toggleHideHandingUserInput() {
    isHideHandingUserInput.value = !isHideHandingUserInput.value
}
function toggleAttributeBindings() {
    isAttributeBindings.value = !isAttributeBindings.value
}
</script>

<template>
    <HandingUserInput v-if="isHideHandingUserInput"/>
    <AttributeBindings v-if="isAttributeBindings"/>
    <div class="hide-button-wrapper">
        <button class="" @click="toggleHideHandingUserInput">HandingUserInput</button>
        <button class="" @click="toggleAttributeBindings">Attribute Bindings</button>
    </div>
</template>

<style>

</style>