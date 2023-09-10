<script setup>
import { ref } from "vue";

const props = defineProps({
  classes: {
    type: String,
    required: false,
    default: "",
  },
});

const count = ref(0);
//TODO: make category count dynamic
</script>

<template>
  <span class="filter-count" :classes="classes">{{ count }}</span>
</template>

<style lang="scss">
.filter-count {
  color: $color-font-second;
  font-size: $font-size-small;
  line-height: $font-size-normal;
}
</style>
