<script setup lang="ts">
import { ref } from 'vue';
import HandingUserInput from '../components/HandlingUserInput.vue';
import AttributeBindings from '../components/AttributeBindings.vue';
import TemperatureConverter from '../components/TemperatureConverter.vue';

const isHideHandingUserInput = ref(false)
const isAttributeBindings = ref(false)
const isTemperatureConverter = ref(false)

function toggleHideHandingUserInput() {
    isHideHandingUserInput.value = !isHideHandingUserInput.value
}
function toggleAttributeBindings() {
    isAttributeBindings.value = !isAttributeBindings.value
}
function toggleTemperatureConverter() {
    isTemperatureConverter.value = !isTemperatureConverter.value
}
</script>

<template>
    <HandingUserInput v-if="isHideHandingUserInput"/>
    <AttributeBindings v-if="isAttributeBindings"/>
    <TemperatureConverter v-if="isTemperatureConverter"/>
    <div class="hide-button-wrapper">
        <button class="" @click="toggleHideHandingUserInput">HandingUserInput</button>
        <button class="" @click="toggleAttributeBindings">Attribute Bindings</button>
        <button class="" @click="toggleTemperatureConverter">Temperature Converter</button>
    </div>
</template>

<style>

</style>