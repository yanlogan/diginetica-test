<script setup>
import { ref, computed } from "vue";
import IconBase from "./IconBase.vue";

const props = defineProps({
  id: {
    type: String,
    required: true,
    default: "",
  },
  showSearchBtn: {
    type: Boolean,
    required: false,
    default: false,
  },
  placeholder: {
    type: String,
    required: false,
    default: "",
  },
  isHeader: {
    type: Boolean,
    required: false,
    default: false,
  },
  classes: {
    type: String,
    required: false,
    default: "",
  },
});

const inputField = ref(null);
const inputValue = ref("");
const isInputNotEmpty = computed(() => inputValue.value.length > 0);

const resetField = () => {
  inputValue.value = "";
  inputField.value.focus();
};
</script>

<template>
  <form class="search" :class="classes">
    <IconBase :name="isHeader ? 'searchHeader' : 'search'" />
    <div class="search__input-wrapper">
      <input
        ref="inputField"
        type="search"
        name=""
        :id="id"
        class="search__input"
        :placeholder="placeholder"
        v-model="inputValue"
      />
      <button
        type="button"
        @click="resetField"
        class="search__resetBtn btn"
        v-show="isInputNotEmpty"
      >
        <IconBase name="remove" :size="isHeader ? 24 : 16" />
      </button>
    </div>
    <button
      type="submit"
      class="search__actionBtn btn"
      v-show="isInputNotEmpty && showSearchBtn"
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
  border: 1px solid $color-border;
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
  margin-left: $gap-header-small;
}
.search__input {
  width: 100%;

  &::placeholder {
    color: $color-font-second;
  }
}
.search__resetBtn,
.search__actionBtn {
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
