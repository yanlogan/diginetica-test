<script setup>
import Header from "./components/Header.vue";
</script>

<template>
  <header class="header-wrapper">
    <Header />
  </header>
  <aside class="filters-wrapper">
    <!-- filters -->
    filters
  </aside>
  <main class="search-results-wrapper">
    <!-- search results -->
    search results
  </main>
</template>

<style scoped>
.header-wrapper {
  grid-area: header;
}
.filters-wrapper {
  grid-area: filters;
}
.search-results-wrapper {
  grid-area: results;
}
</style>
