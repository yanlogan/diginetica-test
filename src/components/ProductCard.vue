<script setup>
import { ref, watchEffect, computed } from "vue";
import defaultImage from "../assets/images/product-default.png";
import IconHot from "./icons/IconHot.vue";
import ProductButton from "./ProductButton.vue";

const props = defineProps({
  title: {
    type: String,
    required: true,
  },
  seller: {
    type: String,
    required: true,
  },
  isInStock: {
    type: Boolean,
    required: true,
    default: true,
  },
  price: {
    type: Number,
    required: true,
    validator: (value) => value >= 0,
  },
  oldPrice: {
    type: Number,
    required: false,
    validator: (value) => value >= 0,
  },
  imageUrl: {
    type: String,
    required: false,
    default: defaultImage,
    validator: (value) => {
      const urlPattern = /^https?:\/\/\S+\.(png|jpe?g|webp|svg)$/i;
      return urlPattern.test(value) || value === defaultImage;
    },
  },
  discount: {
    type: Number,
    required: false,
    validator: (value) => value >= 0 && value <= 100,
  },
  isHot: {
    type: Boolean,
    required: false,
  },
});

const isValidPrice = computed(() => {
  return props.price >= 0;
});

const isValidOldPrice = computed(() => {
  return props.oldPrice >= 0 && props.oldPrice > props.price;
});

const isValidDiscount = computed(() => {
  return props.discount >= 0 && props.discount <= 100;
});

// simulation of a product being sold real-time & changing the inStock status
const isInStock = ref(props.isInStock);

watchEffect(() => {
  isInStock.value = props.isInStock;
});
</script>

<template>
  <div class="product-card" :class="{ 'product-card--sold': !isInStock }">
    <div class="product-card__image">
      <img :src="imageUrl" alt="картинка товара" />
      <div class="product-card__labels">
        <div v-show="isHot" class="product-card__label product-card__isHot">
          <span>Хит продаж</span>
          <IconHot />
        </div>
        <div
          v-show="discount && isValidDiscount"
          class="product-card__label product-card__discount"
        >
          {{ discount }}%
        </div>
      </div>
    </div>
    <div class="product-card__content">
      <div class="product-card__info">
        <div class="product-card__seller">{{ seller }}</div>
        <a class="product-card__title" href="#">{{ title }}</a>
      </div>
      <div class="product-card__bottom">
        <div class="product-card__price" v-show="isInStock">
          <span class="product-card__price-current" v-show="isValidPrice"
            >{{ price }} ₽</span
          >
          <span
            class="product-card__price-old"
            v-show="oldPrice && isValidOldPrice"
          >
            {{ oldPrice }} ₽
          </span>
        </div>
        <div class="product-card__btn">
          <ProductButton name="buy" v-if="isInStock" />
          <ProductButton name="notify" v-else />
        </div>
      </div>
    </div>
  </div>
</template>

<style lang="scss">
$gap: 16px;
$gap-small: calc($gap / 2);
$label-offset: 12px;

.product-card {
  display: grid;
  grid-template-rows: 200px auto;
  gap: $gap;

  &:hover {
    cursor: pointer;

    .product-card__title:not(:visited) {
      color: $color-font-hover;
    }
  }

  &:not(.product-card--sold):hover {
    .product-card__image img {
      transform: scale(1.37);
    }
  }
}

.product-card__image {
  position: relative;
  display: flex;
  align-items: center;
  justify-content: center;
  overflow: hidden;
  background-color: #f8f8fa;

  img {
    max-height: 100%;
    width: auto;
    transition: all 0.3s;
  }
}

.product-card--sold .product-card__image {
  background-color: #fbfbfc;
  img {
    opacity: 0.5;
  }
}

.product-card__labels {
  position: absolute;
  width: 100%;
  height: 100%;
}

.product-card__label {
  position: absolute;
  left: $label-offset;
}

.product-card__isHot {
  top: $label-offset;
  display: flex;
  align-items: center;
  height: 32px;
  padding: 0 $gap-small;
  border: 1px solid $scroll-bar;
  border-radius: 4px;
  background-color: $color-white;

  span {
    margin-right: calc($gap-small / 2);
  }
}

.product-card__discount {
  bottom: $label-offset;
  padding: 6px 10px;
  font-size: $font-size-normal;
  line-height: 100%;
  font-weight: 700;
  color: $color-white;
  border-radius: 4px;
  background-color: $color-brand;
}

.product-card__content,
.product-card__bottom {
  @include list(c, $gap);
}

.product-card__content {
  justify-content: space-between;
}

.product-card__info {
  display: grid;
  gap: $gap-small;
}

.product-card__seller {
  color: $color-font-second;
}

.product-card__title {
  display: -webkit-box;
  -webkit-line-clamp: 2;
  -webkit-box-orient: vertical;
  overflow: hidden;
  text-overflow: ellipsis;

  &:not(:visited):hover {
    color: $color-font-hover;
  }

  &:visited {
    color: $color-font-history;
  }
}

.product-card__price {
  display: flex;
  align-items: center;
}

.product-card__price-current {
  margin-right: $gap-small;
  font-size: $font-size-big;
  line-height: $font-size-normal;
  font-weight: 700;
}

.product-card__price-old {
  font-size: $font-size-small;
  line-height: $font-size-normal;
  color: $color-font-second;
  text-decoration: line-through;
}

.product-card__btn {
  display: flex;
}
</style>
