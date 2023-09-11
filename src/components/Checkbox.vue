<script setup>
import { ref } from "vue";
import IconBase from "./IconBase.vue";

const props = defineProps({
  id: {
    type: Number,
    required: true,
    default: "",
  },
});

const checkboxValue = ref(false);
const toggleCheckbox = () => {
  checkboxValue.value = !checkboxValue.value;
};
</script>

<template>
  <div class="checkbox-wrapper" @click="toggleCheckbox">
    <input
      :id="id"
      type="checkbox"
      class="checkbox__input"
      :checked="checkboxValue"
    />
    <div class="checkbox">
      <IconBase name="checkbox" />
    </div>
  </div>
</template>

<style lang="scss">
$size: 20px;

.checkbox-wrapper {
  width: $size;
  height: $size;
  cursor: pointer;
}

.checkbox {
  width: 100%;
  height: 100%;
  color: $color-brand;
  background-color: $color-white;
  border: 1px solid $color-border;
  border-radius: 3px;
  transition: all 0.1s;

  &:hover {
    border-color: $color-brand;
  }
}

.checkbox__input:checked + .checkbox {
  position: relative;
  border: none;

  .icon {
    opacity: 1;
    transition: all 0.3s;
  }
}

.checkbox__input:not(:checked) + .checkbox .icon {
  opacity: 0;
}
</style>
