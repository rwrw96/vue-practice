<script setup lang="ts">
import { ref } from 'vue';
import HandingUserInput from '../components/HandlingUserInput.vue';
import AttributeBindings from '../components/AttributeBindings.vue';
import TemperatureConverter from '../components/TemperatureConverter.vue';
import SimpleComponent from '../components/SimpleComponent.vue';
import FormBindings from '../components/FormBindings.vue';

const isHideHandingUserInput = ref(false)
const isAttributeBindings = ref(false)
const isTemperatureConverter = ref(false)
const isSimpleComponent = ref(false)
const isFormBindings = ref(false)

function toggleHideHandingUserInput() {
    isHideHandingUserInput.value = !isHideHandingUserInput.value
}
function toggleAttributeBindings() {
    isAttributeBindings.value = !isAttributeBindings.value
}
function toggleTemperatureConverter() {
    isTemperatureConverter.value = !isTemperatureConverter.value
}
function toggleSimpleComponent() {
    isSimpleComponent.value = !isSimpleComponent.value
}
function toggleFormBindings() {
    isFormBindings.value = !isFormBindings.value
}
</script>

<template>
    <HandingUserInput v-if="isHideHandingUserInput"/>
    <AttributeBindings v-if="isAttributeBindings"/>
    <TemperatureConverter v-if="isTemperatureConverter"/>
    <SimpleComponent v-if="isSimpleComponent"/>
    <FormBindings v-if="isFormBindings"/>
    <div class="hide-button-wrapper">
        <button class="" @click="toggleHideHandingUserInput">HandingUserInput</button>
        <button class="" @click="toggleAttributeBindings">Attribute Bindings</button>
        <button class="" @click="toggleTemperatureConverter">Temperature Converter</button>
        <button class="" @click="toggleSimpleComponent">Simple Component</button>
        <button class="" @click="toggleFormBindings">Form Bindings</button>
    </div>
</template>

<style>

</style>