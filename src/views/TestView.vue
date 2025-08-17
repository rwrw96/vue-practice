<script setup lang="ts">
    import { ref, computed, watch, watchEffect, useTemplateRef, onMounted, provide } from 'vue';
    import Test from '../components/Test.vue';
    import slotTest from '../components/slotTest.vue';
    
    const count = ref(0)

    function increment(countTarget) {
        if (countTarget === 'count') {
            count.value++
        } else if (countTarget === 'age') {
            user.value.age++
        }
    }
    function decrement(countTarget) {
        if (countTarget === 'count') {
            count.value--
        } else if (countTarget === 'age') {
            user.value.age--
        }
    }

    const user = ref({
        name: 'Watabe Kazuki',
        age: 30,
        hobbies: {
            reading: [
                '伊坂幸太郎', 
                '湊かなえ'
            ],
            gaming: [
                {
                    'id': 1,
                    'title': 'CODシリーズ',
                    'genre': 'FPS',
                    'description': 'Call of Dutyシリーズは、人気のあるファーストパーソンシューティングゲームです。'
                }, 
                {
                    'id': 2,
                    'title': 'ポケモン',
                    'genre': 'RPG',
                    'description': 'ポケットモンスターシリーズは、ポケモンを捕まえて育てるRPGです。'
                },
            ],
        },
        isOld: false,

    });
    const isOld = computed(() => {
        return user.value.age > 40;
    });

    function alertButton(e) {
        if (e.target.innerText) {
            alert(e.target.innerText + 'がクリックされました');
        } else {
            alert('クリックされました');    
        }

    }

    const text = ref('');
    const checkNames = ref(['dog', 'cat', 'lion']);
    const selected = ref(1);
    const number = ref(0);

    const oldText = ref('');
    const newText = ref('');
    watch(text, (newValue, oldValue) => {
        oldText.value = oldValue;
        newText.value = newValue;
    });

    // watchEffect
    // 明示的に監視対象を書かずに、リアクティブな値を監視する
    const fiveItemsNumber = ref(0);
    watchEffect(() => {
        fiveItemsNumber.value = number.value * 5;
    });

    // useTemplateRef
    // DOM要素にアクセスする
    const numberInput = useTemplateRef('number-input');
    const isYelllow = ref(false);
    function toBeYelllow() {
        if (numberInput.value) {
            isYelllow.value = !isYelllow.value;
            if (isYelllow.value) {
                numberInput.value.style.backgroundColor = 'yellow';
            } else {
                numberInput.value.style.backgroundColor = '';
            }
        }
    }

    const recieivedMessage = ref('');
    const handleMessage = (message) => {
        recieivedMessage.value = message;
    };
    const title = ref('parent title');

    const handleSubmit = ({email, password}) => {
        alert(`登録されました!\nEmail: ${email}\nPassword: ${password}`)
    };

    const childCount = ref(0);

    // provides
    // 親コンポーネントから子コンポーネントへデータを提供する（深い階層を許容）
    const provideMessage = ref('親からのメッセージ');
    provide('provideMessage', provideMessage.value);
</script>

<template>
    <header>
        <div class="wrapper">
            <div class="button-wrapper">
                <button @click="increment('count')">カウントアップボタン</button>
                <button @click="decrement('count')">カウントダウンボタン</button>
                <h1>カウント: {{ count }}</h1>
            </div>
            <div class="user-wrapper">
                <button @click="increment('age')">年齢アップボタン</button>
                <button @click="decrement('age')">年齢ダウンボタン</button>
                <p class="user-name">{{ '名前: '+user.name }}</p>
                <p class="user-age">{{ '年齢: '+user.age }}</p>
                <p class="user-hobby__reading">本: </p>
                <ul v-for="(hobby, index) in user.hobbies.reading" :key="user.id">
                    <li>{{ (index+1) + 'つ目: ' + hobby }}</li>
                </ul>
                <p class="user-hobby__gaming">ゲーム: </p>
                <ul v-for="({title, genre, description}, index) in user.hobbies.gaming" :key="user.id">
                    <li>{{ (index+1) + 'つ目: ' + title }}</li>
                    <li>{{ 'ジャンル: ' + genre }}</li>
                    <li>{{ '説明: ' + description }}</li>
                </ul>
                <p v-if="isOld" :class="{'isOld': isOld}">この人は歳をとっています</p>
                <p v-else>この人は若いです</p>
                <button @click="alertButton">アラートボタン</button>
                <input type="text" @keyup.enter="alertButton" placeholder="Enterキーでアラート" v-model="text" />
                <p class="input-text">{{ '先ほど入力された: ' + oldText }}</p>
                <p class="input-text">{{ '新しく入力された: ' + newText }}</p>
                <input type="checkbox" value="dog" v-model="checkNames" />
                <label for="dog">dog</label>
                <input type="checkbox" value="cat" v-model="checkNames" />
                <label for="cat">cat</label>
                <input type="checkbox" value="lion" v-model="checkNames" />
                <label for="lion">lion</label>
                <ul>
                    <li v-for="checkName in checkNames">{{ checkName }}</li>
                </ul>
                <select v-model="selected">
                    <option :value="1">1</option>
                    <option :value="2">2</option>
                    <option :value="3">3</option>
                </select>
                <p>選択された値: {{ selected }}</p>
                <input type="number" v-model.number="number" />
                <p>入力された数値*5: {{ fiveItemsNumber }}</p>

                <input type="number" ref="number-input" />
                <button @click="toBeYelllow">黄色にするボタン</button>
            </div>
        </div>
        <button @click="childCount++">親側の子供カウントボタン</button>
        <p>親側の子供カウント: {{ childCount }}</p>
    </header>
    <Test :title=title  @message="handleMessage" @submit="handleSubmit" v-model:="childCount" class="isChild" style="background-color: bisque;" />
    <p>{{ recieivedMessage }}</p>
    <slotTest>
        <template #first>
            <h1>一つ目: これはslotテストです</h1>
        </template>
        <template #secound>
            <h2>二つ目: これはslotテストです</h2>
        </template>
        <template #third></template>
    </slotTest>
</template>

<style scoped>
button {
    margin: 0 20px;
}
.isOld {
    margin-top: 20px;
    color: red;
    font-weight: bold;
}
label {
    margin-right: 10px;
}
</style>