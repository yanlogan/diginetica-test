<script setup>
import { computed } from "vue";
import FilterSection from "./FilterSection.vue";
import IconBase from "./IconBase.vue";

const props = defineProps({
  categories: {
    type: Array,
    required: true,
    default: () => [],
  },
});

const categories = computed(() => {
  return props.categories;
});

//TODO: make category count dynamic
</script>

<template>
  <FilterSection classes="filter-categories">
    <ul class="filter-categories__list">
      <li v-for="category in categories" :key="category.id">
        <a
          :href="category.url"
          class="filter-category"
          :class="{ 'filter-category--parent': category.children }"
        >
          <div>
            <IconBase name="back" v-show="category.children" />
            <span class="filter-category__title">{{ category.title }}</span>
          </div>

          <span class="filter-category__count">3</span>
        </a>
        <ul v-show="category.children">
          <li
            v-for="childCategory in category.children"
            :key="childCategory.id"
          >
            <a
              :href="childCategory.url"
              class="filter-category filter-category--child"
            >
              <span class="filter-category__title">{{
                childCategory.title
              }}</span>

              <span class="filter-category__count">3</span>
            </a>
          </li>
        </ul>
      </li>
    </ul>
  </FilterSection>
</template>

<style lang="scss">
.filter-categories__list {
  & > li > a {
    padding: 0 16px 0 8px;
  }

  & ul > li > a {
    padding: 0 16px 0 calc(32px - 8px);
  }
}
.filter-category {
  // position: relative;
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 100%;
  height: 30px;
  border-radius: 5px;

  &--parent {
    & > div {
      display: flex;
      align-items: center;
    }
  }

  &:hover {
    color: $color-brand;
  }
  &:active {
    color: $color-font-main;
    background-color: $color-font-bg;
  }
}
//TODO: make title overflow ??
// .filter-category__title {
// position: absolute;
// white-space: nowrap;
// overflow: visible;
// }

.filter-category__count {
  color: $color-font-second;
  font-size: $font-size-small;
  line-height: $font-size-normal;
}
</style>
