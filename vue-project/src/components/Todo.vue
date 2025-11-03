<script setup>
import { query , collection, getDocs, doc } from 'firebase/firestore';
import {ref , onMounted } from 'vue'
import db from '../firebase/init.js'


const todos = ref([])
async function getToDos() {
    const coll = collection(db, 'todos') 
    const querySnap = await getDocs(query(coll))
    todos.value = []
    querySnap.forEach((doc) => {
        let data = doc.data()
        data.id = doc.id
        todos.value.push(data)
    })
}
onMounted(() => {
    getToDos()
}

)


</script>
 
<template>
<div>
    <ul>
        <li v-for="todo in todos" :key ="todo.title">
            {{todo.title}}
        </li> 
    

    </ul>
</div>
</template>
 
<style scoped>

</style>