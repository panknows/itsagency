<template lang="pug">
div(class="good")
  a(class="good__link", href="/")
  div(class="good__head")
    div(class="good__head-content")
      img(class="good__image", :src="GoodImage")
  div(class="good__body")
    p(class="good__title") Краска Wallquest, Brownsone MS90102
  div(class="good__footer")
    div(class="good__price") 4800 ₽
    div(class="good__slot")
      slot
</template>

<script setup lang="ts">
import GoodImage from "./good.png";
</script>

<style lang="scss">
.good {
  position: relative;

  &__link {
    position: absolute;
    inset: 0;
  }

  &__head {
    position: relative;
    display: flex;
    align-items: center;
    justify-items: center;

    &:before {
      content: "";
      padding-top: 100%;
      display: block;
    }

    &-content {
      display: flex;
      align-items: center;
      justify-content: center;
      width: 100%;
    }
  }

  &__image {
    max-width: 100%;
    height: auto;
  }

  &__body {
    padding-top: 16px;
  }

  &__title {
    font-size: 16px;
    font-weight: 300;
    text-align: left;
    color: #1f2020;
    line-height: 18px;
  }

  &__footer {
    padding-top: 20px;
    display: flex;
    align-items: center;
    justify-content: space-between;

    @media (min-width: 1024px) {
      padding-top: 24px;
    }
  }

  &__price {
    font-size: 16px;
    font-weight: 600;
    line-height: 16px;
  }

  &__slot {
    z-index: 2;
  }
}
</style>
