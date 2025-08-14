<script setup>
    import { ref } from 'vue';
    const description = ref("これはテストコンポーネントです。Vueのコンポーネントの基本的な構造を示しています。");
    const heading = ref("heading");

    const objectOfAttrs = {
        id: 'container',
        class: 'p-content',
        style: 'background-color:green'
    };
</script>

<template>
    <div class="wrapper">
        <h1 :class="heading">Test Component</h1>
        <p v-bind="objectOfAttrs">
            {{ description }}
        </p>
    </div>
</template>

<style scoped>
.heading {
    color: blue;
    padding: 20px;
    font-size: 24px;
    font-weight: bold;
}
.p-content {
    color: white;
    padding: 10px;
    font-size: 16px;
    border-radius: 5px;
}
</style>