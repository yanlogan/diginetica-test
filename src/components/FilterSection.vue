<script setup>
const props = defineProps({
  classes: {
    type: String,
    required: false,
    default: "",
  },
  title: {
    type: String,
    required: false,
    default: "",
  },
  needsClearSelection: {
    type: Boolean,
    required: false,
    default: false,
  },
});
</script>

<template>
  <section class="filter-section" :class="classes">
    <header
      class="filter-section__header"
      :class="{ 'filter-section__header--clear': needsClearSelection }"
      v-show="title"
    >
      <span class="filter-section__title" v-show="title">{{ title }}</span>
      <button
        class="filter-section__clearSelectionBtn"
        v-show="needsClearSelection"
      >
        Очистить
      </button>
    </header>
    <slot></slot>
  </section>
</template>

<style lang="scss">
.filter-section {
  margin-bottom: 28px;

  ul {
    @include list(c);
  }
}

.filter-section__header {
  display: flex;
  justify-content: center;
  margin-bottom: 16px;

  &--clear {
    justify-content: space-between;
  }
}

.filter-section__title {
  font-size: $font-size-big;
  line-height: 125%;
  font-weight: 700;
}

.filter-section__clearSelectionBtn {
  color: $color-font-second;
  font-size: $font-size-small;
  line-height: 100%;
  text-decoration: underline;

  &:hover,
  &:active {
    color: $color-font-main;
  }
}
</style>
