<script setup>
import { ref, onMounted } from "vue";
import axios from "axios";
import CategoryCard from "../CategoryCard.vue";


const categories = ref([]);

async function getCategoriesData() {
    try {
        const response = await axios.get('https://zullkit-backend.demo.belajarkoding.com/api/categories?limit=4')
        console.log(response.data.data)
        categories.value = response.data.data.data
    } catch (error) {
        console.error(error)
    }


}

onMounted(() => {
    getCategoriesData()
})

</script>

<template>
    <div class="container px-4 mx-auto my-16 md:px-12" id="categories">
        <h2 class="mb-4 text-xl font-medium md:mb-0 md:text-lg">Top Categories</h2>
        <div class="flex flex-wrap -mx-1 lg:-mx-4">
            <CategoryCard v-for="cat in categories" :key="cat.id" :id="cat.id" :title="cat.name" :count="cat.products_count"
                :image="cat.thumbnails" />
        </div>
    </div>
</template>
