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
  clearSelection: {
    type: Boolean,
    required: false,
    default: false,
  },
});

const resetForms = (e) => {
  const insideForms = document.querySelectorAll(".filter-section form");

  e.target.reset();

  insideForms.forEach((form) => {
    form.reset();
  });
};
</script>

<template>
  <form class="filter-section" :class="classes" @reset="resetForms">
    <header
      class="filter-section__header"
      :class="{ 'filter-section__header--clear': clearSelection }"
      v-show="title"
    >
      <span class="filter-section__title" v-show="title">{{ title }}</span>
      <button
        type="reset"
        class="filter-section__clearSelectionBtn"
        v-show="clearSelection"
      >
        Очистить
      </button>
    </header>
    <slot></slot>
  </form>
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
  align-items: baseline;
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
