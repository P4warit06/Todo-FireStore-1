<script setup>
import { ref, onMounted,watch } from 'vue'
import { collection, getDocs,query,where} from 'firebase/firestore'
import db from '../firebase/init.js'
import { useRoute } from "vue-router"
import QueryList from '../components/QueryList.vue'
import ProductList from '../components/ProductList.vue'

const category = ref()
const products = ref([])
const route = useRoute()
async function getProducts() {
    category.value = route.params.category
    try {
        let q
        if (category.value) {
            q = query(collection(db, "myproducts"), where("category", "==", category.value))
        } else {
            q = query(collection(db, "myproducts"))
        }
        const querySnapshot = await getDocs(q)
        products.value = querySnapshot.docs.map(doc => ({
            id: doc.id,
            ...doc.data()
        }))
    } catch (error) {
        console.error("Error fetching products:", error)
    }
}

onMounted(() => {
    getProducts()
})

watch( () => route.params.category, getProducts)

</script>

<template>
    <QueryList :category="category" />
    <ProductList :category="category" :products="products" />
</template>

<style scoped>
 
</style>

