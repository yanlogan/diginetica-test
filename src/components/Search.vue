<script setup>
import { ref, computed } from "vue";
import IconBase from "./IconBase.vue";

const inputField = ref(null);
const inputValue = ref("");
const isInputNotEmpty = computed(() => inputValue.value.length > 0);

const resetForm = () => {
  inputValue.value = "";
  inputField.value.focus();
};
</script>

<template>
  <form class="search" @reset="resetForm">
    <IconBase name="search" />
    <div class="search__input-wrapper">
      <input
        ref="inputField"
        type="search"
        name="header-search"
        id="header-search"
        class="search__input"
        placeholder="Поиск по 100 000 товаров"
        v-model="inputValue"
      />
      <button
        type="reset"
        class="search__resetBtn btn"
        v-show="isInputNotEmpty"
      >
        <IconBase name="remove" />
      </button>
    </div>
    <button
      type="submit"
      class="search__actionBtn btn"
      v-show="isInputNotEmpty"
    >
      Найти
    </button>
  </form>
</template>

<style lang="scss">
.search {
  display: flex;
  align-items: center;
  flex-grow: 1;
  margin: 0 $gap-header;
  padding: 4px 4px 4px 16px;
  border: 1px solid $color-border;
  border-radius: 10px;
  transition: all 0.3s;

  &:hover,
  &:focus-within {
    border-color: $color-border-hover;
  }
}
.search__input-wrapper {
  display: flex;
  align-items: center;
  flex-grow: 1;
  margin: 0 $gap-header-small;
}
.search__input {
  width: 100%;
  line-height: 150%;

  &::placeholder {
    color: $color-font-second;
  }
}
.search__resetBtn {
  margin-left: $gap-header-small;
}
.search__actionBtn {
  padding: 12px 16px;
  font-family: "PT Sans", sans-serif;
  font-weight: 700;
  line-height: 100%;
  color: $color-white;
  background-color: $color-border-hover;
  border-radius: $gap-header-small;
}
</style>
