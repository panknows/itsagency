<template lang="pug">
div(class="app")
  div(class="app__header")
    AppHeader
  div(class="app__hero")
    div(class="app__hero-container container")
      div(class="app__breadcrumbs") breadcrumbs
    div(class="app__carousel") carousel
  div(class="app__container container")
    div(class="app__body")
      div(class="app__content")
        div(class="app__left")
          div(class="app__filters")
            BaseToggle(v-for="label in ['Новинки', 'Есть в наличии', 'Контрактные', 'Эксклюзивные', 'Распродажа']" :key="label" :label="label" :model-value="false")
        div(class="app__right")
          div(class="app__sort") sort
          div(class="app__items")
            div(class="app__item")
              GoodCard
                template(#default)
                  AddGoodToCardButton(@click="addToCart")
            div(class="app__item")
              GoodCard
                template(#default)
                  AddGoodToCardButton(@click="addToCart")
  div(class="app__footer")
</template>

<script setup lang="ts">
import { AppHeader } from "@/widgets/AppHeader";
import { GoodCard } from "@/entities/good";

import { AddGoodToCardButton } from "@/features/add-good-to-cart";

import { BaseToggle } from "@/shared/ui/base";

const addToCart = () => console.log("add");
</script>

<style lang="scss">
.app {
  display: flex;
  flex-direction: column;
  min-height: 100vh;

  &__filters {
    display: flex;
    flex-direction: column;
    gap: 10px;
  }
  &__footer {
    background: #000;
    height: 100px;
    margin-top: auto;
  }
  &__breadcrumbs {
  }
  &__hero {
  }
  &__content {
    display: flex;
    flex-direction: column;
    gap: 24px;

    @media (min-width: 1024px) {
      flex-direction: row;
    }
  }
  &__body {
    padding-top: 48px;

    @media (min-width: 1024px) {
      padding-top: 72px;
    }
  }

  &__left {
    @media (min-width: 1024px) {
      max-width: 279px;
      width: 100%;
    }
  }
  &__right {
    display: flex;
    flex-direction: column;
    gap: 24px;

    @media (min-width: 1024px) {
      gap: 44px;
    }
  }
  &__items {
    display: grid;
    grid-template-columns: repeat(2, minmax(0, 1fr));
    gap: 24px 14px;
    width: 100%;

    @media (min-width: 1024px) {
      gap: 24px;
      grid-template-columns: repeat(4, minmax(0, 1fr));
    }
    @media (min-width: 1440px) {
      grid-template-columns: repeat(5, minmax(0, 1fr));
    }
  }
  &__item {
    padding-bottom: 34px;
    border-bottom: 1px solid #0000001a;
    grid-column: span 1 / span 1;

    &:nth-last-child(2) {
      border-bottom: 0;
    }
    &:nth-last-child(1) {
      border-bottom: 0;
    }

    @media (min-width: 1024px) {
      &:nth-last-child(3) {
        border-bottom: 0;
      }
      &:nth-last-child(4) {
        border-bottom: 0;
      }
    }
    @media (min-width: 1440px) {
      &:nth-last-child(5) {
        border-bottom: 0;
      }
    }
  }
}
</style>
