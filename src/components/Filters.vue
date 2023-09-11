<script setup>
import { computed } from "vue";
import FilterCategories from "./FilterCategories.vue";
import FilterPrice from "./FilterPrice.vue";
import FilterCheckbox from "./FilterCheckbox.vue";

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
  sizes: {
    type: Array,
    required: true,
    default: () => [],
  },
});

//TODO: change FilterCategories on currentCategory update

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
    <FilterCheckbox
      title="Бренд"
      :clear-selection="true"
      :source="sellers"
      :search="true"
    />
    <FilterCheckbox title="Размер" :source="sizes" />
  </section>
</template>

<style lang="scss"></style>
