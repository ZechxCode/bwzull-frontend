<script setup>
import { onMounted, computed } from 'vue'
import { useUserStore } from '../../stores/user';

import UserInfo from './UserInfo.vue'

import Logo from './Logo.vue'
import NavLinks from './NavigationLinks.vue'
import AuthButton from './AuthButton.vue';

const userStore = useUserStore()
const getUser = computed(() => userStore.getUser)
const isLoggedin = computed(() => userStore.isLoggedIn)

onMounted(() => {
    userStore.fetchUser()
})
</script>

<template>
    <nav class="bg-white border-gray-200 px-2 sm:px-4 py-2.5 rounded dark:bg-gray-800">
        <div class="container flex flex-wrap items-center justify-between mx-auto my-2">
            <Logo />
            <UserInfo v-if="isLoggedin" :user="getUser.data" />
            <AuthButton v-else />
            <NavLinks />
        </div>
    </nav>
</template>