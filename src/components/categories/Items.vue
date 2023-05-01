<script setup>
import { ref, onMounted } from 'vue'
import { useRoute } from 'vue-router'
import axios from 'axios';

import NewItemsCard from '../NewItemsCard.vue';

const NewItems = ref([])
const category = ref([])
const route = useRoute()

async function getItemsData() {
    try {
        const response = await axios.get('https://zullkit-backend.demo.belajarkoding.com/api/categories?id=' + route.params.id + '&show_product=1')
        console.log(response.data.data)
        NewItems.value = response.data.data.products
        category.value = response.data.data
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
        <h2 class="mb-4 text-xl font-medium md:mb-0 md:text-lg">{{ category.name }}</h2>
        <div class="flex flex-wrap -mx-1 lg:-mx-4">
            <NewItemsCard v-for="newItem in NewItems" :key="newItem.id" :id="newItem.id" :title="newItem.name"
                :subcat="newItem.subtitle" :image="newItem.thumbnails" />

        </div>
    </div>
</template>