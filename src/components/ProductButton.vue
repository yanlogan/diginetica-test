<script>
import ProductBuyButton from "./ProductBuyButton.vue";
import ProductNotifyButton from "./ProductNotifyButton.vue";

const buttons = {
  buy: ProductBuyButton,
  notify: ProductNotifyButton,
};

export default {
  props: {
    name: {
      type: String,
      required: true,
      validator(value) {
        return Object.prototype.hasOwnProperty.call(buttons, value);
      },
    },
  },

  computed: {
    buttonComponent() {
      return buttons[this.name];
    },
  },
};
</script>

<template>
  <component
    :is="buttonComponent"
    :id="`product-btn-${name}`"
    :class="`product__btn product__btn--${name} btn`"
    role="button"
  ></component>
</template>

<style lang="scss">
.product__btn {
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 11px 15px;
  font-weight: 700;
  font-size: $font-size-normal;
  line-height: 100%;
  border: 1px solid $color-border;
  border-radius: 4px;
}
.product__btn--buy {
  color: $color-brand;
  border-color: $color-brand;

  &:hover {
    color: $color-white;
    background-color: $color-brand;
  }
}
.product__btn--notify {
  width: 100%;
  color: $color-font-second;
  border-color: $color-font-second;

  @include mobile {
    padding: 11px 0;
  }
}
</style>
