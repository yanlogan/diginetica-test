<script setup>
import { computed } from "vue";
import ProductCard from "./ProductCard.vue";

const props = defineProps({
  source: {
    type: Array,
    required: true,
    default: () => [],
  },
  categoryTitle: {
    type: String,
    required: true,
    default: "",
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
  <section class="search-results-wrapper">
    <h2 class="category__title">{{ categoryTitle }}</h2>
    <div class="search-results">
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
    </div>
  </section>
</template>

<style lang="scss">
$gap: 24px;
$gap-mobile: calc($gap / 2);

.category__title {
  display: none;

  @include mobile {
    display: block;
    margin-bottom: calc($gap / 2);
    font-size: 22px;
    line-height: 28px;
  }
}

.search-results {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: $gap;

  @include laptop {
    grid-template-columns: repeat(3, 1fr);
  }

  @include tablet {
    grid-template-columns: repeat(2, 1fr);
  }

  @include mobile {
    gap: 16px $gap-mobile;
  }
}
</style>
