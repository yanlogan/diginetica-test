<script setup>
import Checkbox from "./Checkbox.vue";
import FilterCount from "./FilterCount.vue";
import FilterSection from "./FilterSection.vue";
import Search from "./Search.vue";

const props = defineProps({
  source: {
    type: Array,
    required: true,
    default: () => [],
  },
  search: {
    type: Boolean,
    required: false,
    default: false,
  },
  title: {
    type: String,
    required: false,
    default: "",
  },
  clearSelection: {
    type: Boolean,
    required: false,
    default: false,
  },
});

//TODO: implement search
</script>

<template>
  <FilterSection
    classes="filter-checkbox"
    :title="title"
    :clear-selection="clearSelection"
  >
    <Search
      id="filter-checkbox-search"
      :show-search-btn="false"
      classes="filter-checkbox__search"
      placeholder="Поиск"
      v-show="search"
    />
    <div :class="{ 'filter-checkbox__search-results': search }">
      <ul class="filter-checkbox__list">
        <li
          v-for="option in source"
          :key="option.id"
          class="filter-checkbox__option"
        >
          <Checkbox :labeled="true">
            <span class="filter-checkbox__option-title">{{
              option.title
            }}</span>
            <FilterCount classes="filter-checkbox__option-count"
          /></Checkbox>
        </li>
      </ul>
    </div>
  </FilterSection>
</template>

<style lang="scss">
.filter-checkbox__search-results {
  position: relative;
  height: 180px;
  overflow-y: auto;
}
.filter-checkbox__search {
  padding: 9px 11px;
  margin-bottom: 16px;
  border-radius: 4px;
}

ul.filter-checkbox__list {
  @include list(c, 12px);
}

.filter-checkbox__option {
  @include list;
  align-items: center;

  .checkbox__label {
    width: 100%;
    padding-right: 16px;
  }
}

.filter-checkbox__option-title {
  flex-grow: 1;
  margin-left: 12px;
}
</style>
