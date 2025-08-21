<script setup>
import { ref, computed } from 'vue';

const users = ref([
    {
        'surname': 'tanaka',
        'name': 'taro'
    },
    {
        'surname': 'suzuki',
        'name': 'jiro'
    },
    {
        'surname': 'miyamoto',
        'name': 'kenji'
    }
]);

const userText = ref('');
const userSurname = ref('');
const userName = ref('');
const selectedUser = ref([]);

// 前方一致検索
const filteredUsers = computed(() => {
    return users.value.filter(
        (user) => !(user.name+", "+user.surname).indexOf(userText.value)
    )
});

// ユーザー新規作成
function createUser(name, surname) {
    if (!name || !surname) return false;
    users.value.push({"surname": surname, "name": name});
    userSurname.value = '';
    userName.value = '';
}

// ユーザー更新
function updateUser(name, surname) {
    if (!name || !surname) return false;
    selectedUser.value.name = name;
    selectedUser.value.surname = surname;
    userSurname.value = '';
    userName.value = '';
}

// ユーザー削除
function deleteUser() {
    users.value = users.value.filter(user => user !== selectedUser.value);
}
</script>

<template>
    <div class="wrapper">
        <div class="filter-wrapper">
            <input type="text" v-model="userText" placeholder="filter" >
        </div>
        <div class="name-wrapper">
            <select size="4" v-model="selectedUser">
                <option :value=user v-for="user in filteredUsers">
                    {{ user.name }}, {{ user.surname }}
                </option>
            </select>
            <div class="name-form">
                <label for="">name:</label>
                <input type="text" v-model="userName">    
                <label for="">Surname:</label>
                <input type="text" v-model="userSurname">
            </div>
        </div>
        <div class="button-wrapper">
            <button @click="createUser(userName, userSurname)">create</button>
            <button @click="updateUser(userName, userSurname)">update</button>
            <button @click="deleteUser()">delete</button>
        </div>
    </div>
</template>

<style>
.name-wrapper {
    display: flex;   
    select {
        width: 200px;
        margin-right: 30px;
    }
}
.name-form {
    display: flex;
    flex-direction: column;
}
</style>