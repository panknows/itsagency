<template>
  <div class="cart-good">
    <img :src="GoodImage" alt="Product Image" class="cart-good__image" />
    <div class="cart-good__info">
      <div class="cart-good__title">{{ title }}</div>
      <div class="cart-good__price">{{ price }} ₽</div>
    </div>
    <div class="cart-good__stepper">
      <BaseNumericStepper v-model="quantity" />
    </div>
    <button @click="removeItem" class="cart-good__remove-button">
      <img :src="XIcon" alt="" />
    </button>
  </div>
</template>

<script lang="ts" setup>
import { ref, defineProps, defineEmits } from "vue";

import GoodImage from "./good.png";
import XIcon from "@/shared/assets/icons/x.svg";
import { BaseNumericStepper } from "@/shared/ui/base";

const props = defineProps<{
  imageSrc: string;
  title: string;
  price: number;
  initialQuantity?: number;
}>();

const emit = defineEmits<{
  (e: "remove"): void;
}>();

const quantity = ref(props.initialQuantity || 1);

const removeItem = () => {
  emit("remove");
};
</script>

<style lang="scss">
.cart-good {
  display: flex;
  align-items: center;
  padding: 12px 0;

  &__image {
    width: 96px;
    min-width: 96px;
    height: 96px;
    margin-right: 8px;
  }

  &__info {
    flex: 1;
    display: flex;
    flex-direction: column;
    max-width: 165px;
  }

  &__title {
    margin-bottom: 16px;
    font-size: 16px;
    font-weight: 300;
    line-height: 18px;
  }

  &__price {
    font-size: 16px;
    font-weight: 600;
    line-height: 16px;
  }

  &__stepper {
    margin-right: 37px;
    margin-left: auto;
  }

  &__remove-button {
    background-color: transparent;
    border: none;
    font-size: 16px;
    cursor: pointer;
    color: #ff5f5f;
    opacity: 0.2;
  }
}
</style>
