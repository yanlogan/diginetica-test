<script>
import IconSearchHeader from "./icons/IconSearchHeader.vue";
import IconSearch from "./icons/IconSearch.vue";
import IconRemove from "./icons/IconRemove.vue";
import IconClose from "./icons/IconClose.vue";
import IconDropdown from "./icons/IconDropdown.vue";
import IconArrow from "./icons/IconArrow.vue";
import IconBack from "./icons/IconBack.vue";
import IconHot from "./icons/IconHot.vue";
import IconCheckbox from "./icons/IconCheckbox.vue";

const icons = {
  search: IconSearch,
  searchHeader: IconSearchHeader,
  remove: IconRemove,
  close: IconClose,
  dropdown: IconDropdown,
  arrow: IconArrow,
  back: IconBack,
  hot: IconHot,
  checkbox: IconCheckbox,
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
    size: {
      type: Number,
      required: false,
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
    <component :is="iconComponent" role="presentation" :size="size" />
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
