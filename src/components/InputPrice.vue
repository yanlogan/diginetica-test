<script setup>
import { ref, computed, onMounted } from "vue";

const priceInput = ref(null);
const price = ref(5500);
const minPrice = 0;
const maxPrice = 10000000;

const props = defineProps({
  classes: {
    type: String,
    required: false,
    default: "",
  },
  id: {
    type: String,
    required: true,
    default: "",
  },
  placeholder: {
    type: String,
    required: false,
    default: "0",
  },
  label: {
    type: String,
    required: true,
    default: "",
  },
});

const formattedPrice = computed(() => {
  return price.value.toString().replace(/\B(?=(\d{3})+(?!\d))/g, " ");
});

const updatePrice = (e) => {
  const input = parseInt(e.target.value.replace(/\s/g, ""));

  if (isNaN(input)) {
    price.value = minPrice;
  } else price.value = input;

  resizeInput();
};

const setDefaultPrice = (e) => {
  if (e.target.value === "") {
    e.target.value = minPrice;
  }
};

const validateInput = (e) => {
  const keyCode = e.keyCode || e.which;
  const keyValue = String.fromCharCode(keyCode);
  const isValidInput = /^\d+$/.test(keyValue); // check if it's a number
  const inputValue = e.target.value.replace(/\s/g, "") + keyValue;
  const inputNumber = parseInt(inputValue);

  if (!isValidInput || inputNumber < minPrice || inputNumber > maxPrice) {
    e.preventDefault();
  }
};

const resizeInput = function () {
  if (!priceInput.value) return;

  const tempEl = document.createElement("span");
  tempEl.innerText = formattedPrice.value;
  tempEl.style.fontFamily = window.getComputedStyle(
    priceInput.value
  ).fontFamily;
  tempEl.style.fontSize = window.getComputedStyle(priceInput.value).fontSize;
  tempEl.style.padding = window.getComputedStyle(priceInput.value).padding;
  document.body.appendChild(tempEl);
  const width = tempEl.getBoundingClientRect().width;
  document.body.removeChild(tempEl);
  priceInput.value.style.width = `${width}px`;
};

onMounted(() => {
  resizeInput();
});
</script>

<template>
  <div class="price-input" :class="classes">
    <label :for="id">{{ label }}</label>
    <input
      type="text"
      ref="priceInput"
      :id="id"
      :placeholder="placeholder"
      :value="formattedPrice"
      @input="updatePrice"
      @blur="setDefaultPrice"
      @keypress="validateInput"
    />
    <span>₽</span>
  </div>
</template>

<style lang="scss">
.price-input {
  position: relative;
  display: flex;
  align-items: center;
  width: 100%;
  padding: 10px 8px;
  background-color: $color-white;
  border: 1px solid $color-border;
  border-radius: 4px;
}

.price-input input {
  width: 100%;
  margin-right: 6px;
}

.price-input label {
  margin-right: 6px;
  font-size: $font-size-small;
  line-height: $font-size-normal;
  color: $color-font-second;
}
</style>
