<template lang="pug">
div(class="dropdown")
  div(class="dropdown__toggle")
    slot(name="trigger" v-bind="{ toggle, selectedOption }")
  div(v-if="isOpen" class="dropdown__menu" @click.stop)
    ul(class="dropdown__options")
      li(
        v-for="option in options"
        :key="option.value"
        class="dropdown__option"
        :class="{ _selected: option.value === modelValue }"
        @click="selectOption(option)"
      ) {{ option.label }}
  div(v-if="isOpen" class="dropdown__overlay" @click="close")
</template>

<script lang="ts" setup>
import {
  ref,
  defineProps,
  defineEmits,
  computed,
  onMounted,
  onBeforeUnmount,
} from "vue";

interface Option {
  label: string;
  value: string | number;
}

const props = defineProps<{
  modelValue: string | number | null;
  options: Option[];
}>();

const emit = defineEmits<{
  (e: "update:modelValue", value: string | number): void;
}>();

const isOpen = ref(false);

const toggle = () => {
  isOpen.value = !isOpen.value;
};

const close = () => {
  isOpen.value = false;
};

const selectOption = (option: Option) => {
  emit("update:modelValue", option.value);
  close();
};

// Найти выбранную опцию для отображения
const selectedOption = computed(
  () =>
    props.options.find((option) => option.value === props.modelValue) || null
);

// Закрытие при клике вне компонента
const handleOutsideClick = (event: MouseEvent) => {
  if (!(event.target as HTMLElement).closest(".dropdown")) {
    close();
  }
  onMounted(() => {
    document.addEventListener("click", handleOutsideClick);
  });

  onBeforeUnmount(() => {
    document.removeEventListener("click", handleOutsideClick);
  });
};
</script>

<style scoped lang="scss">
.dropdown {
  position: relative;
  display: inline-block;
}

.dropdown__overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  background-color: rgba(0, 0, 0, 0.7);
  z-index: 99;
}

.dropdown__menu {
  position: absolute;
  top: 0;
  right: 0;
  min-width: 280px;
  background-color: #fff;
  z-index: 100;
}

.dropdown__options {
  list-style: none;
  margin: 0;
  padding: 0;
}

.dropdown__option {
  padding: 16px 24px;
  cursor: pointer;
  font-size: 12px;
  font-weight: 500;
  line-height: 15px;
  text-transform: uppercase;

  &._selected {
    background: #7bb899;
  }
}
</style>
