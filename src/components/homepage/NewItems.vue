<script setup>
import { ref, onMounted } from 'vue'
import NewItemsCard from '../NewItemsCard.vue';

import axios from 'axios';


const NewItems = ref([])

async function getItemsData() {
    try {
        const response = await axios.get('https://zullkit-backend.demo.belajarkoding.com/api/products')
        console.log(response.data.data)
        NewItems.value = response.data.data.data
    } catch (error) {
        console.error(error)
    }
}

onMounted(() => {
    getItemsData()
})

</script>

<template>
    <div class="container px-4 mx-auto my-16 md:px-12">
        <h2 class="mb-4 text-xl font-medium md:mb-0 md:text-lg">New Items</h2>
        <div class="flex flex-wrap -mx-1 lg:-mx-4">
            <NewItemsCard v-for="newItem in NewItems" :key="newItem.id" :id="newItem.id" :title="newItem.name"
                :subcat="newItem.subtitle" :image="newItem.thumbnails" />

        </div>
    </div>
</template>