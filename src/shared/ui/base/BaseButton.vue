<template>
  <button :class="['button', variantClass]" @click="handleClick">
    <slot></slot>
  </button>
</template>

<script lang="ts" setup>
import { defineProps, defineEmits, computed } from "vue";

const props = defineProps<{
  variant?: "primary";
  disabled?: boolean;
}>();

const emit = defineEmits<{
  (e: "click"): void;
}>();

const handleClick = () => {
  if (!props.disabled) {
    emit("click");
  }
};

const variantClass = computed(() => {
  return props.variant ? `_${props.variant}` : "_primary";
});
</script>

<style scoped lang="scss">
.button {
  padding: 20px 16px;
  font-size: 12px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  transition: background-color 0.3s;
  font-weight: 500;
  line-height: 15px;

  &._primary {
    background-color: #7bb899;
    color: #1f2020;
    text-transform: uppercase;
  }

  &:disabled {
    background-color: #ccc;
    cursor: not-allowed;
  }
}
</style>
