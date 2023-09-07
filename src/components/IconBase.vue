<script>
import IconSearch from "./icons/IconSearch.vue";
import IconRemove from "./icons/IconRemove.vue";
import IconClose from "./icons/IconClose.vue";
import IconDropdown from "./icons/IconDropdown.vue";
import IconArrow from "./icons/IconArrow.vue";
import IconHot from "./icons/IconHot.vue";

const icons = {
  search: IconSearch,
  remove: IconRemove,
  close: IconClose,
  dropdown: IconDropdown,
  arrow: IconArrow,
  hot: IconHot,
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

.icon-remove,
.icon-close {
  &:hover {
    svg > g {
      opacity: 1;
    }
  }
}
.icon-dropdown--active {
  transform: rotate(180deg);
}
</style>
