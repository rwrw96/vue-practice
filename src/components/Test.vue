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
            default: 'Child Component'
        }
    });

    // defineEmits
    // 子コンポーネントから親コンポーネントへイベントを送信するための定義
    const emit = defineEmits({
        message: null,
        submit: null, 
    });
    
    const sendMessage = () => {
        emit('message', 'Hello from Test Component!');
    };

    const email = ref('');
    const password = ref('');
    const sendSubmit = () => {
        // バリデーションチェック
        if (!email.value || !password.value) {
            alert('Email and password are required!');
            return;
        }
        emit('submit', {email: email.value, password: password.value});
    }
</script>

<template>
    <div class="wrapper">
        <h1 :class="heading">{{ title }}</h1>
        <p v-bind="objectOfAttrs">
            {{ description }}
        </p>
        <button @click="sendMessage">メッセージを送信</button>
        <form @submit.prevent="sendSubmit" class="email-password">
            email: <input type="text" v-model="email">
            password: <input type="password" v-model="password">
            <button type="submit">登録</button>
        </form> 
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
.email-password {
    display: flex;
    flex-direction: column;
    gap: 10px;
    width: 200px;
}
</style>