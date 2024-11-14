<template lang="pug">
button(class="addGoodToCartButton")
  img(:src="PlusIcon")
</template>

<script setup lang="ts">
import PlusIcon from "@/shared/assets/icons/plus.svg";
</script>

<style lang="scss">
.addGoodToCartButton {
  background: #f2f2f2;
  width: 40px;
  height: 24px;
  border-radius: 6px;
  border: 0;
  display: flex;
  align-items: center;
  justify-content: center;

  @media (min-width: 1024px) {
    width: 80px;
    height: 32px;
    border-radius: 8px;
    background: #7bb899;
  }
}
</style>
