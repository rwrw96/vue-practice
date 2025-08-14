<script setup>
    import { ref } from 'vue';
    const description = ref("これはテストコンポーネントです。Vueのコンポーネントの基本的な構造を示しています。");
    const heading = ref("heading");

    const objectOfAttrs = {
        id: 'container',
        class: 'p-content',
        style: 'background-color:green'
    };

    // defineProps
    // 親コンポーネントから受け取るpropsの定義
    defineProps({
        title: {
            type: String,
            default: 'Test Component'
        }
    });

    // defineEmits
    // 子コンポーネントから親コンポーネントへイベントを送信するための定義
    const emit = defineEmits(['message']);
    const sendMessage = () => {
        emit('message', 'Hello from Test Component!');
    };
</script>

<template>
    <div class="wrapper">
        <h1 :class="heading">{{ title }}</h1>
        <p v-bind="objectOfAttrs">
            {{ description }}
        </p>
        <button @click="sendMessage">メッセージを送信</button>
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