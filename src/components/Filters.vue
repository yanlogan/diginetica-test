<script setup>
import { ref, computed } from "vue";
import FilterCategories from "./FilterCategories.vue";
import FilterPrice from "./FilterPrice.vue";
import FilterSeller from "./FilterSeller.vue";
import FilterSize from "./FilterSize.vue";

const props = defineProps({
  categories: {
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
</script>

<template>
  <section class="filters">
    <FilterCategories :categories="categories" />
    <FilterPrice />
    <FilterSeller />
    <FilterSize />
  </section>
</template>

<style lang="scss"></style>
