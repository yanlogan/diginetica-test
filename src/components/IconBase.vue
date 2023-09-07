<script>
import IconSearch from "./icons/IconSearch.vue";
import IconRemove from "./icons/IconRemove.vue";

const icons = {
  search: IconSearch,
  remove: IconRemove,
};

export default {
  props: {
    name: {
      type: String,
      required: true,
      validator(value) {
        return Object.prototype.hasOwnProperty.call(icons, value);
      },
    },
  },

  computed: {
    iconComponent() {
      return icons[this.name];
    },
  },
};
</script>

<template>
  <i class="icon" :class="`icon-${name}`">
    <component :is="iconComponent" role="presentation" />
  </i>
</template>

<style lang="scss">
.icon {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  svg * {
    transition: all 0.3s;
  }
}

.icon-remove:hover {
  svg > g {
    opacity: 1;
  }
}
</style>
