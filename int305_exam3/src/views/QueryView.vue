<script setup>
import { ref, onMounted, watch } from 'vue'
import { arrayRemove, collection, deleteDoc, doc, getDocs, limit, orderBy, query, updateDoc, where ,deleteField, increment, addDoc, arrayUnion } from 'firebase/firestore'
import db from '../firebase/init.js'
import { useRoute } from "vue-router"
import QueryList from '../components/QueryList.vue'
import ProductList from '../components/ProductList.vue'

const category = ref('')
const products = ref([])
const heading = ref('')
const route = useRoute()

async function getQuery() {
    const qryId = route.params.qryId
    products.value = []
    let qry = null
    if (qryId == 1) {
        heading.value = 'Update iPhone 17 Pro Max price to 1199'
        category.value = ''  
        const qryRef = doc(db, 'myproducts', 'iPhone17')
        await updateDoc(qryRef, { price: 1199 })
    } else if (qryId == 2) {
        heading.value = 'Add Color Blue to Iphone 17 Pro Max'
        category.value = ''
        const docRef = doc(db, 'myproducts', 'iPhone17')
        await updateDoc(docRef, { color: arrayUnion('Blue')})
        
    } else if (qryId == 3) {
        heading.value = "Decrease the iPhone 17 Pro Max price by 100"
        category.value = ''
        const docRef = doc(db, 'myproducts', 'iPhone17')
        await updateDoc(docRef, {price: increment(-100)})
    }
    else if (qryId == 4) { 
        heading.value = 'Add Storage Size field to the iPhone 17 Pro Max with 1TB'
        const docRef = doc(db, 'myproducts', 'iPhone17')
        await updateDoc(docRef,{storageSize : '1TB'})
    }else if (qryId == 5) {
        heading.value = 'Remove Storage Size field to the iPhone 17 Pro Max'
        const docRef = doc(db, 'myproducts', 'iPhone17')
        await updateDoc(docRef, { storageSize: deleteField() })
    } else if (qryId == 6) {
        heading.value = 'Remove the book title MongoDB The Definitive Guide'
        category.value = ''
        const docRef = doc(db, 'myproducts', "mongodb")
        await deleteDoc(docRef)
    } else if (qryId == 7) {
        heading.value = 'Remove Color Silver in the iPhone 17 Pro Max'
        const docRef = doc(db, 'myproducts', 'iPhone17')
        await updateDoc(docRef, {color:arrayRemove("Silver")})
    }

    // else if (qryId == 2) {
    //     heading.value = 'Update Iphone 17 '
    //     const qryRef = doc(db, 'myproducts', 'NImkYDEir4B00YflOggU')
    //     await updateDoc(qryRef, { price: 48000 })
    //     return;
    // } else if (qryId == 3) {
    //     heading.value = "Delete Iphone 17"
    //     const qryRef = doc(db, 'myproducts', 'NImkYDEir4B00YflOggU')
    //     await deleteDoc(qryRef)
    //     return
    // } else if (qryId == 4) {
    //     heading.value = "Sort by title (desc)"
    //     category.value = ''
    //     qry = query(collection(db, "myproducts"), orderBy("title", "desc"))
    //     const snapshot = await getDocs(qry)
    //     products.value = snapshot.docs.map(doc => ({
    //         id: doc.id,
    //         ...doc.data(),
    //     }))
    // } else if (qryId == 5) {
    //     heading.value = "A Fiction"
    //     qry = query(
    //         collection(db, "myproducts"),
    //         where('category', '==', 'Books'),
    //         where('keywords', 'array-contains', 'Fiction')
    //     )
    //     const snapshot = await getDocs(qry)
    //     products.value = snapshot.docs.map(doc => ({
    //         id: doc.id,
    //         ...doc.data(),
    //     }))
    //     return
    // } else if (qryId == 6) {
    //     heading.value = "Book Word 'Life'"
    //     qry = query(
    //         collection(db, 'myproducts'),
    //         where('category', '==', 'Books'),
    //         where('keywords', 'array-contains', 'Life')
    //     )
    //     const snapshot = await getDocs(qry)
    //     products.value = snapshot.docs.map(doc => ({
    //         id: doc.id,
    //         ...doc.data(),
    //     }))
    //     return
    // } else if (qryId == 7) {
    //     heading.value = "Book Page Between 300 and 400 (Sort by pages)"
    //     qry = query(
    //         collection(db, "myproducts"),
    //         where('category', '==', 'Books'),
    //         where('pages', '>=', 300),
    //         where('pages', '<=', 400),
    //         orderBy('pages', 'asc')
    //     )
    //     const snapshot = await getDocs(qry)
    //     products.value = snapshot.docs.map(doc => ({
    //         id: doc.id,
    //         ...doc.data(),
    //     }))
    //     return
    // }
    // else if (qryId == 8) {
    //     heading.value = "( Bestseller or Award ) and price less than 20 USD "
    //     qry = query(
    //         collection(db, "myproducts"),
    //         where('category', '==', 'Books'),
    //         where('price', '<=', 20),
    //         where('keywords', 'array-contains-any', ['Bestseller', 'Award'])
    //     )
    //     const snapshot = await getDocs(qry)
    //     products.value = snapshot.docs.map(doc => ({
    //         id: doc.id,
    //         ...doc.data(),
    //     }))
    //     return
    // } else if (qryId == 9) {
    //     heading.value = "Samsung"
    //     qry = query(
    //         collection(db, "myproducts"),
    //         where('category', '==', 'Phones'),
    //         where('brand', '==', 'Samsung'),
    //     )
    //     const snapshot = await getDocs(qry)
    //     products.value = snapshot.docs.map(doc => ({
    //         id: doc.id,
    //         ...doc.data(),
    //     }))
    //     return
    // } else if (qryId == 10) {
    //     heading.value = "Apple price less than 600 "
    //     qry = query(
    //         collection(db, "myproducts"),
    //         where('category', '==', 'Phones'),
    //         where('brand', '==', 'Apple'),
    //         where('price', '<=', 600)
    //     )
    //     const snapshot = await getDocs(qry)
    //     products.value = snapshot.docs.map(doc => ({
    //         id: doc.id,
    //         ...doc.data(),
    //     }))
    //     return
    // } else if (qryId == 11) {
    //     heading.value = "Color Silver Or Red"
    //     qry = query(
    //         collection(db, "myproducts"),
    //         where('category', '==', 'Phones'),
    //         where('colors','array-contains-any',['Silver','Red'])
    //     )
    //     const snapshot = await getDocs(qry)
    //     products.value = snapshot.docs.map(doc => ({
    //         id: doc.id,
    //         ...doc.data(),
    //     }))
    //     return
    // }else if (qryId == 12) {
    //     heading.value = "Apple Max Price"
    //     qry = query(
    //         collection(db, "myproducts"),
    //         where('category', '==', 'Phones'),
    //         where('brand', '==', 'Apple'),
    //         orderBy('price', 'desc'),
    //         limit(1)
    //     )
    //     const snapshot = await getDocs(qry)
    //     products.value = snapshot.docs.map(doc => ({
    //         id: doc.id,
    //         ...doc.data(),
    //     }))
    //     return
    // }
}

onMounted(() => {
    getQuery()
})

watch(() => route.params.qryId, getQuery)

</script>

<template>
    <QueryList :category="category" />
    <h1>{{ heading }}</h1>
    <ProductList :category="category" :products="products" />
</template>

<style scoped>
h1 {
    text-align: center;
    color: blue;
}
</style>