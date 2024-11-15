<template>
  <div>
    <slot name="trigger" v-bind="{ open }" />

    <!-- Overlay -->
    <div v-if="isVisible" class="slideover__overlay" @click="close"></div>

    <!-- SlideOver Panel -->
    <div v-if="isVisible" class="slideover__panel">
      <div class="slideover__header">
        <h3 class="slideover__title">{{ title }}</h3>
        <button @click="close" class="slideover__close-btn">
          <img :src="XIcon" alt="" />
        </button>
      </div>
      <div class="slideover__content">
        <slot />
      </div>
    </div>
  </div>
</template>

<script lang="ts" setup>
import { ref, defineProps, defineEmits } from "vue";

import XIcon from "@/shared/assets/icons/x.svg";

const props = defineProps<{
  title?: string;
}>();

const emit = defineEmits<{
  (e: "open"): void;
  (e: "close"): void;
}>();

const isVisible = ref(true);

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
.slideover {
  &__overlay {
    position: fixed;
    top: 0;
    left: 0;
    width: 100vw;
    height: 100vh;
    background-color: rgba(0, 0, 0, 0.7);
    z-index: 1000;
  }
  &__panel {
    position: fixed;
    top: 0;
    right: 0;
    width: 600px;
    height: 100vh;
    background-color: #fff;
    z-index: 1001;
    transform: translateX(100%);
    animation: slideIn 0.3s forwards;
    display: flex;
    flex-direction: column;
  }
  &__header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding-top: 40px;
    padding-left: 40px;
    padding-right: 40px;
  }
  &__title {
    font-size: 30px;
    font-weight: 500;
    line-height: 26px;
  }
  &__close-btn {
    height: 48px;
    width: 48px;
    border-radius: 50%;
    border: 1px solid rgba(0, 0, 0, 0.1);
    display: flex;
    align-items: center;
    justify-content: center;
    background: none;
    cursor: pointer;
  }
  &__content {
    padding-top: 80px;
    padding-left: 40px;
    padding-right: 40px;
    padding-bottom: 40px;
    overflow-y: auto;
    flex: 1;
  }
}

@keyframes slideIn {
  from {
    transform: translateX(100%);
  }
  to {
    transform: translateX(0);
  }
}
</style>
