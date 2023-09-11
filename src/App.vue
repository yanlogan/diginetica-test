<script setup>
import { ref } from "vue";
import Header from "./components/Header.vue";
import Filters from "./components/Filters.vue";
import SearchResults from "./components/SearchResults.vue";

import products from "./data/products.json";
import categories from "./data/categories.json";
import sellers from "./data/sellers.json";
import sizes from "./data/sizes.json";

const currentCategory = ref(categories[0]);
</script>

<template>
  <header class="header-wrapper">
    <Header />
  </header>
  <aside class="filters-wrapper">
    <Filters :categories="categories" :sellers="sellers" :sizes="sizes" />
  </aside>
  <main class="search-results-wrapper">
    <SearchResults :source="products" :category-title="currentCategory.title" />
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

  @include mobile {
    grid-template-columns: 100%;
    grid-template-areas:
      "header"
      "results";
    gap: calc($gap-row / 2) 0;
    padding: 0 16px;
  }
}

.header-wrapper {
  grid-area: header;
}
.filters-wrapper {
  grid-area: filters;

  @include mobile {
    display: none;
  }
}
.search-results-wrapper {
  grid-area: results;
}
</style>
