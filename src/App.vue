<script setup>
import Header from "./components/Header.vue";
import SearchResults from "./components/SearchResults.vue";

import products from "./data/products.json";
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
    <SearchResults :source="products" />
  </main>
</template>

<style lang="scss">
$padding: 100px;
$gap-row: 24px;
$gap-column: 36px;

#app {
  display: grid;
  grid-template-areas:
    "header header"
    "filters results";
  grid-template-columns: 280px auto;
  gap: $gap-row $gap-column;
  max-width: calc(1720px + $padding * 2);
  margin: 0 auto;
  padding: 0 $padding $gap-column;
}

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
