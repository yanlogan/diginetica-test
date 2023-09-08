<script setup>
import { computed } from "vue";
import ProductCard from "./ProductCard.vue";

const props = defineProps({
  source: {
    type: Array,
    required: true,
    default: () => [],
  },
});

const searchResults = computed(() => {
  return props.source.map((product) => {
    return Object.fromEntries(
      Object.entries(product).filter(([key, value]) => value !== "")
    );
  });
});
</script>

<template>
  <section class="search-results">
    <ProductCard
      v-for="product in searchResults"
      :key="product.id"
      :title="product.title"
      :seller="product.seller"
      :imageUrl="product.imageUrl"
      :price="product.price"
      :old-price="product.oldPrice"
      :is-in-stock="product.isInStock"
      :discount="product.discount"
      :is-hot="product.isHot"
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
