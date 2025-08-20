<script setup>
import { ref } from 'vue';

const textInput = ref('');
const isChecked = ref(false);
const checkedName = ref([]);
const radioButoon = ref('One');
const selected = ref('A');
const multiSelected = ref('A');
</script>

<template>
    <div class="wrapper">
        <h1>Text Input</h1>
        <input type="text" v-model="textInput">
        <p>{{ textInput }}</p>
        <h1>Check box</h1>
        <label><input type="checkbox" v-model="isChecked">checked: {{ isChecked }}</label>
        <h1>Multi Checkbox</h1>
        <label><input type="checkbox" value="Jack" v-model="checkedName">Jack</label>
        <label><input type="checkbox" value="John" v-model="checkedName">John</label>
        <label><input type="checkbox" value="Mike" v-model="checkedName">Mike</label>
        {{ checkedName }}
        <h1>Radio</h1>
        <label><input type="radio" value="One" v-model="radioButoon">One</label>
        <label><input type="radio" value="Two" v-model="radioButoon">Two</label>
        picked: {{ radioButoon }}
        <h1>Select</h1>
        <select v-model="selected">
            <option value="" disabled>defaut</option>
            <option value="A">A</option>
            <option value="B">B</option>
            <option value="C">C</option>
        </select>
        Selected: {{ selected }}
        <h1>Multi Select</h1>
        <select v-model="multiSelected" multiple>
            <option value="A">A</option>
            <option value="B">B</option>
            <option value="C">C</option>
        </select>
        Selected: {{ multiSelected }}
    </div>
</template>