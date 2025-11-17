<script setup>
import { RouterLink } from 'vue-router'
const props = defineProps({
  category: {
    type: String,
    required: true,
  }
});
</script>

<template>
    <div class="menu">
        <RouterLink class="new" to="/products/add">Add Product</RouterLink>
        <RouterLink class="item" to="/query/1">Update iPhone 17 Pro Max price to 1199</RouterLink>
        <RouterLink class="item" to="/query/2">Add Color 'Blue' to Iphone 17 Pro Max</RouterLink>
        <RouterLink class="item" to="/query/3">Decrease the iPhone 17 Pro Max price by 100 </RouterLink>
        <RouterLink class="item" to="/query/4">Add 'Storage Size' field to the iPhone 17 Pro Max with 1TB</RouterLink>
        <RouterLink class="item" to="/query/5">Remove 'Storage Size' field to the iPhone 17 Pro Max </RouterLink>
        <RouterLink class="item" to="/query/6">Remove the book title 'MongoDB The Definitive Guide'</RouterLink>
        <RouterLink class="item" to="/query/7">Remove Color 'Silver' in the iPhone 17 Pro Max </RouterLink>
        <template v-if="props.category==''">
            <RouterLink class="item" to="/query/1">Sort by price</RouterLink>

            <!--  RouteLink for querying All  -->

        </template>

        <template v-if="props.category=='Books'">
            <RouterLink class="item" to="/query/5">Fiction </RouterLink>
            <RouterLink class="item" to="/query/6">Word "Life" </RouterLink>
            <RouterLink class="item" to="/query/7">#page Between 300 and 400 (Sort by Pages) </RouterLink>
            <RouterLink class="item" to="/query/8">( Bestseller or Award ) and price less than 20 USD </RouterLink>
        </template>

        <template v-if="props.category=='Phones'">
            <RouterLink class="item" to="/query/9">Samsung</RouterLink>
            <RouterLink class="item" to="/query/10">Apple price less than 600 USD </RouterLink>
            <RouterLink class="item" to="/query/11">Silver or Red</RouterLink>
            <RouterLink class="item" to="/query/12">Apple max price</RouterLink>
        </template>
    </div>
</template>

<style scoped>
    a {
        text-decoration: none ;
    }
    .menu {
        display: flex ;
        flex-wrap: wrap ;
    }
    .item, .new {
        background-color: #ffd580 ;
        border: 1px solid black ;
        border-radius: 25px ;
        text-align: center ;
        font-size: smaller ;
        margin: 2px ;
        padding: 5px ;
    }
    .new {
        background-color: rgb(0,180,0) ;
        color: white ;
    }
</style>