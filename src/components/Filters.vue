<script setup>
import { ref, computed } from "vue";
import FilterCategories from "./FilterCategories.vue";
import FilterPrice from "./FilterPrice.vue";
import FilterSellers from "./FilterSellers.vue";
import FilterSize from "./FilterSize.vue";

const props = defineProps({
  categories: {
    type: Array,
    required: true,
    default: () => [],
  },
  sellers: {
    type: Array,
    required: true,
    default: () => [],
  },
});

//TODO: change FilterCategories on currentCategory update
// const currentCategory = ref("");

const categories = computed(() => {
  return props.categories.filter((category) => {
    return category.title !== ""; // && category.url !== ""
  });
});

const sellers = computed(() => {
  return props.sellers;
});
</script>

<template>
  <section class="filters">
    <FilterCategories :categories="categories" />
    <FilterPrice />
    <FilterSellers :sellers="sellers" />
    <FilterSize />
  </section>
</template>

<style lang="scss"></style>
