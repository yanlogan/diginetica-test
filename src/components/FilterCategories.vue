<script setup>
import { ref, computed } from "vue";
import FilterSection from "./FilterSection.vue";
import FilterCount from "./FilterCount.vue";
import IconBase from "./IconBase.vue";

const props = defineProps({
  currentCategory: {
    type: Object,
    required: true,
    default: () => {},
  },
  categories: {
    type: Array,
    required: true,
    default: () => [],
  },
});

const categories = computed(() => {
  return props.categories;
});

const isTopLevel = ref(false);
</script>

<template>
  <FilterSection classes="filter-categories">
    <ul class="filter-categories__list">
      <li v-for="category in categories" :key="category.id">
        <a
          :href="category.url"
          class="filter-category"
          :class="{
            'filter-category--parent': category.children,
            active: props.currentCategory.id === category.id,
            'filter-category--top-level': isTopLevel,
          }"
        >
          <div>
            <IconBase name="back" v-show="category.children && !isTopLevel" />
            <span class="filter-category__title">{{ category.title }}</span>
          </div>

          <FilterCount classes="filter-category__count" />
        </a>
        <ul v-show="category.children">
          <li
            v-for="childCategory in category.children"
            :key="childCategory.id"
          >
            <a
              :href="childCategory.url"
              class="filter-category filter-category--child"
              :class="{
                active: props.currentCategory.id === childCategory.id,
              }"
            >
              <span class="filter-category__title">{{
                childCategory.title
              }}</span>

              <FilterCount classes="filter-category__count" />
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

  ul > li > a {
    padding: 0 16px 0 32px;
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
  &:active,
  &.active {
    color: $color-font-main;
    background-color: $color-font-bg;

    .filter-category__count {
      color: $color-font-main;
    }
  }

  &.active:hover {
    color: $color-font-main;
  }
}
//TODO: make title overflow ??
// .filter-category__title {
// position: absolute;
// white-space: nowrap;
// overflow: visible;
// }
</style>
