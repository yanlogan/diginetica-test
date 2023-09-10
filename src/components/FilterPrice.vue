<script setup>
import FilterSection from "./FilterSection.vue";
import InputPrice from "./InputPrice.vue";
</script>

<template>
  <FilterSection classes="filter-price" title="Цена">
    <div class="filter-price-wrapper">
      <InputPrice classes="filter-price__input" id="price-from" label="от" />
      <div class="filter-price__divider"></div>
      <InputPrice classes="filter-price__input" id="price-to" label="до" />
    </div>
  </FilterSection>
</template>

<style lang="scss">
.filter-price-wrapper {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
.filter-price__divider {
  width: 10px;
  height: 1px;
  margin: 0 16px;
  flex-shrink: 0;
  background-color: $color-border;
}
</style>
