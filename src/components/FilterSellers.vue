<script setup>
import { computed } from "vue";
import Checkbox from "./Checkbox.vue";
import FilterCount from "./FilterCount.vue";
import FilterSection from "./FilterSection.vue";
import Search from "./Search.vue";

const props = defineProps({
  sellers: {
    type: Array,
    required: true,
    default: () => [],
  },
});

const sellers = computed(() => {
  return props.sellers;
});

//TODO: implement search
</script>

<template>
  <FilterSection classes="filter-sellers" title="Бренд" :clear-selection="true">
    <Search
      id="filter-sellers-search"
      :show-search-btn="false"
      classes="filter-sellers__search"
      placeholder="Поиск"
    />
    <div class="filter-sellers__search-results">
      <ul class="filter-sellers__list">
        <li v-for="seller in sellers" :key="seller.id" class="filter-seller">
          <Checkbox :id="seller.id" />
          <label :for="seller.id">
            <span class="filter-seller__title">{{ seller.title }}</span>
            <FilterCount classes="filter-seller__count" />
          </label>
        </li>
      </ul>
    </div>
  </FilterSection>
</template>

<style lang="scss">
.filter-sellers__search-results {
  height: 180px;
  overflow-y: scroll;
}
.filter-sellers__search {
  padding: 9px 11px;
  margin-bottom: 16px;
  border-radius: 4px;
}

ul.filter-sellers__list {
  @include list(c, 12px);
}

.filter-seller {
  @include list;
  align-items: center;

  label {
    @include list;
    align-items: center;
    width: 100%;
    padding-right: 16px;
    cursor: pointer;
  }
}

.filter-seller__title {
  flex-grow: 1;
  margin-left: 12px;
}
</style>
