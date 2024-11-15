<template>
  <div class="numeric-stepper">
    <button
      @click="decrement"
      class="numeric-stepper__button"
      :disabled="modelValue <= 1"
    >
      <img :src="MinusIcon" alt="" />
    </button>
    <div class="numeric-stepper__amount">
      {{ modelValue }}
    </div>
    <button @click="increment" class="numeric-stepper__button">
      <img :src="PlusIcon" alt="" />
    </button>
  </div>
</template>

<script lang="ts" setup>
import { defineProps, defineEmits } from "vue";

import PlusIcon from "@/shared/assets/icons/plus.svg";
import MinusIcon from "@/shared/assets/icons/minus.svg";

const props = defineProps<{
  modelValue: number;
  min?: number;
  max?: number;
  step?: number;
}>();

const emit = defineEmits<{
  (e: "update:modelValue", value: number): void;
}>();

const increment = () => {
  const newValue = props.modelValue + (props.step || 1);
  if (props.max === undefined || newValue <= props.max) {
    emit("update:modelValue", newValue);
  }
};

const decrement = () => {
  const newValue = props.modelValue - (props.step || 1);
  if (newValue >= 0) {
    emit("update:modelValue", newValue);
  }
};
</script>

<style scoped lang="scss">
.numeric-stepper {
  display: flex;
  align-items: center;
  gap: 16px;

  &__amount {
    font-size: 16px;
    font-weight: 400;
    line-height: 16px;
    min-width: 20px;
    display: flex;
    justify-content: center;
  }

  &__button {
    background-color: #f2f2f2;
    border: none;
    cursor: pointer;
    border-radius: 4px;
    width: 40px;
    height: 24px;
    display: flex;
    justify-content: center;
    align-items: center;

    &:disabled {
      background-color: #ccc;
      cursor: not-allowed;
    }

    img {
      width: 16px;
    }
  }
}
</style>
