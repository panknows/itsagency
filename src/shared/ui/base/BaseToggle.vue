<template>
  <label class="switch">
    <input
      type="checkbox"
      class="switch__input"
      :checked="isActive"
      @input="toggle"
    />
    <span class="switch__container">
      <span class="switch__box" :class="{ _active: isActive }">
        <span class="switch__slider" :class="{ _active: isActive }"></span>
      </span>
      <span v-if="label" class="switch__label">{{ label }}</span>
    </span>
  </label>
</template>

<script lang="ts" setup>
import { ref, defineProps, defineEmits, watch } from "vue";

const props = withDefaults(
  defineProps<{
    modelValue: boolean;
    label?: string;
  }>(),
  {
    label: "",
  }
);

const emit = defineEmits<{
  (e: "update:modelValue", value: boolean): void;
}>();

const isActive = ref(props.modelValue);

const toggle = () => {
  isActive.value = !isActive.value;
  emit("update:modelValue", isActive.value);
};

// Следим за изменением modelValue из родителя
watch(
  () => props.modelValue,
  (newValue) => {
    isActive.value = newValue;
  }
);
</script>

<style lang="scss" scoped>
.switch {
  $width: 36px;
  $innerOffset: 7px;

  &__input {
    position: absolute;
    width: 1px;
    height: 1px;
    padding: 0;
    margin: -1px;
    overflow: hidden;
    clip: rect(0, 0, 0, 0);
    border: 0;
  }

  &__container {
    display: flex;
    align-items: center;
    gap: 8px;
    cursor: pointer;
  }

  &__box {
    width: $width;
    height: 22px;
    background-color: #f2f2f2;
    border-radius: 40px;
    display: flex;
    align-items: center;
    transition: background-color 0.3s;
    position: relative;
    box-sizing: border-box;

    &._active {
      background-color: #7bb899;
    }
  }

  &__slider {
    width: 8px;
    min-width: 8px;
    height: 8px;
    background-color: #1f2020;
    border-radius: 50%;
    transition: transform 0.3s;
    position: relative;
    transform: translateX($innerOffset);

    &._active {
      transform: translateX(calc($width - $innerOffset - 100%));
    }
  }

  &__label {
    font-size: 12px;
    font-weight: 400;
    line-height: 12px;
    color: #1f2020;
    text-transform: uppercase;
  }
}
</style>
