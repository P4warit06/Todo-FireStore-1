<script setup>
import { RouterLink, RouterView } from "vue-router";
</script>

<template>
  <div id="header">
    <h2>Reports</h2>
    <RouterLink to="/query/1">
      <div class="QueryExample">
        1. Cities with population &gt; 10,000
      </div>
    </RouterLink>
    <RouterLink to="/query/2">
      <div class="QueryExample">
        2. Cities in Flodia (FL)
      </div>
    </RouterLink>

    <RouterLink to="/query/3">
      <div class="QueryPractice">
        3. List zips in DC with population > 40,000
      </div>
    </RouterLink>
    <RouterLink to="/query/4">
      <div class="QueryPractice">
        4. List zips in FL or in DC with population> 60000
      </div>
    </RouterLink>
    <RouterLink to="/query/5">
      <div class="QueryPractice">
        5. List zips in DC or cities with population > 100,000.
      </div>
    </RouterLink>

    <RouterLink to="/query/6">
      <div class="QueryPractice">
        6. List zips in DC and sort the data by population.
      </div>
    </RouterLink>
    <RouterLink to="/query/7">
      <div class="QueryPractice">
        7. List zips latitude (x) between 71 and 73.
      </div>
    </RouterLink>
  </div>
  <div id="detail">
    <RouterView />
  </div>
</template>

<style scoped>
.header {
  color: white;
}

a {
  display: block;
}

.QueryExample {
  font-weight: bolder;
  color: #693CBD
}

.QueryPractice {
  font-weight: bolder;
  font-family: sans-serif;
  color: #2B8899;
}
</style>
