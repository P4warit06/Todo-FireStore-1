<script setup>
// Importing components
import HelloWorld from './components/HelloWorld.vue'
import TheWelcome from './components/TheWelcome.vue'
import ToDo from './components/Todo.vue'
</script>

<template>
  <!-- Header Section -->
  <header class="app-header">
    <!-- Vue Logo -->
    <img alt="Vue logo" class="logo" src="./assets/logo.svg" width="125" height="125" />

    <!-- Welcome Message -->
    <div class="wrapper">
      <HelloWorld msg="You did it Pawarit!" />
    </div>
  </header>

  <!-- Main Content Section -->
  <main class="app-main">
    <!-- Uncomment TheWelcome component if needed -->
    <!-- <TheWelcome /> -->

    <!-- ToDo Component -->
    <ToDo />
  </main>
</template>

<style scoped>
/* Scoped styles for App.vue */

/* Header styling */
.app-header {
  margin-bottom: 20px;
}

/* Main content styling */
.app-main {
  background-color: #3854e2;
  margin-left : 12  px;  
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}
</style>