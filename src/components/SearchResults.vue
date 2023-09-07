<script setup>
import ProductCard from "./ProductCard.vue";
</script>

<template>
  <section class="search-results">
    <ProductCard
      title="Полное название товара в несколько строк для вида с обрывом в конце..."
      seller="Бренд"
      :price="5990"
      :old-price="5990"
      :is-in-stock="true"
      :discount="25"
      :is-hot="true"
    />
    <ProductCard
      title="Полное название товара в несколько строк для вида с обрывом в конце..."
      seller="Бренд"
      :price="5990"
      :old-price="5990"
      :is-in-stock="false"
      :discount="25"
      :is-hot="true"
    />
  </section>
</template>

<style lang="scss">
$gap: 24px;
$gap-mobile: calc($gap / 2);

.search-results {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: $gap;
}
</style>
