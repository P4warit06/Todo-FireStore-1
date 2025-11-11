<script setup>
import { RouterView } from 'vue-router'
import { ref, onMounted } from 'vue'
import { query, collection, getDocs, getDoc } from 'firebase/firestore'
import db from './firebase/init.js'
import CategoryList from './components/CategoryList.vue'

const categories = ref([])

async function getCategories() {
  try {
    const q = query(collection(db, "mycategories"))
    const querySnapshot = await getDocs(q)
    categories.value = querySnapshot.docs.map(doc => ({
      id: doc.id,
      ...doc.data()
    }))
  } catch (error) {
    console.error("Error fetching categories:", error)
  }
}

onMounted(() => {
    getCategories()
})
</script>

<template>
  <CategoryList :categories="categories"/>
  <div class="content">
    <RouterView />
  </div>
</template>

<style scoped>

</style>
