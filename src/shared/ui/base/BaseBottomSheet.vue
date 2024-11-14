<template lang="pug">
div
  slot(name="trigger", v-bind="{ open }")

  div(v-if="isVisible" class="bottom-sheet-overlay" @click="close")
    div(class="bottom-sheet" @click.stop)
      div(class="bottom-sheet__header")
        button(@click="close" class="bottom-sheet__close-btn")
      div(class="bottom-sheet__content")
        slot
</template>

<script lang="ts" setup>
import { ref, defineProps, defineEmits } from "vue";

const props = defineProps<{
  title?: string;
}>();

const emit = defineEmits<{
  (e: "open"): void;
  (e: "close"): void;
}>();

const isVisible = ref(false);

const open = () => {
  isVisible.value = true;
  emit("open");
};

const close = () => {
  isVisible.value = false;
  emit("close");
};
</script>

<style scoped lang="scss">
.bottom-sheet-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  display: flex;
  justify-content: center;
  align-items: flex-end;
  z-index: 1000;
}

.bottom-sheet {
  width: 100%;
  max-width: 500px;
  background-color: #fff;
  border-radius: 24px 24px 0 0;
  padding: 12px 24px;
  box-shadow: 0 -2px 10px rgba(0, 0, 0, 0.2);
  animation: slideUp 0.3s ease;

  &__header {
    display: flex;
    align-items: center;
  }

  &__title {
    font-size: 18px;
    margin: 0;
  }

  &__close-btn {
    border: none;
    cursor: pointer;
    width: 28px;
    height: 4px;
    border-radius: 40px;
    opacity: 0.6;
    background: #1f2020;
    margin: 0 auto;
  }

  &__content {
    margin-top: 16px;
  }
}

@keyframes slideUp {
  from {
    transform: translateY(100%);
  }
  to {
    transform: translateY(0);
  }
}
</style>
