<script setup>
import { ref, onMounted } from "vue";
import axios from "axios";
import CategoryCard from "../CategoryCard.vue";


const categories = ref([]);

async function getCategoriesData() {
    try {
        const response = await axios.get('https://zullkit-backend.demo.belajarkoding.com/api/categories?limit=1000')
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
        <h2 class="mb-4 text-xl font-medium md:mb-0 md:text-lg">All Categories</h2>
        <div class="flex flex-wrap -mx-1 lg:-mx-4">
            <CategoryCard v-for="cate in categories" :key="cate.id" :id="cate.id" :title="cate.name"
                :count="cate.products_count" :image="cate.thumbnails" />
        </div>
    </div>
</template>
