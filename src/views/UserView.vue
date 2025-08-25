<script setup lang="ts">
import { useUserStore } from '@/stores/user'

const user = useUserStore()
</script>

<template>
    <div>
        {{ user }}
        <input type="text" v-model="user.name" >
    </div>
</template>