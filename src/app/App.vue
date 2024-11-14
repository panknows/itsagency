<template lang="pug">
div(class="app")
  div(class="app__header")
    AppHeader
  div(class="app__hero")
    div(class="app__hero-container container")
      div(class="app__breadcrumbs")
        BaseBreadcrumbs(:breadcrumbs="[{ label: 'Главная', url: '/' },{ label: 'Продукты', url: '/' },{ label: 'Краски' }]")
      h1(class="app__header") Краски
    div(class="app__carousel") carousel
  div(class="app__container container")
    div(class="app__body")
      div(class="app__content")
        div(class="app__left")
          div(class="app__filters")
            BaseToggle(v-for="label in ['Новинки', 'Есть в наличии', 'Контрактные', 'Эксклюзивные', 'Распродажа']" :key="label" :label="label" :model-value="false")
        div(class="app__right")
          div(class="app__controls")
            div(class="app__total-items") 412 товаров
            button(class="app__filters-bottom-sheet") Фильтры
            button(class="app__sort") Сначала дорогие
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

import { BaseToggle, BaseBreadcrumbs } from "@/shared/ui/base";

const addToCart = () => console.log("add");
</script>

<style lang="scss">
.app {
  display: flex;
  flex-direction: column;
  min-height: 100vh;

  &__filters {
    display: none;
    flex-direction: column;
    gap: 10px;

    @media (min-width: 1024px) {
      display: flex;
    }
  }
  &__footer {
    background: #000;
    height: 100px;
    margin-top: auto;
  }
  &__breadcrumbs {
  }
  &__hero {
    padding-top: 16px;

    @media (min-width: 1024px) {
      padding-top: 0;
    }

    &-container {
      display: flex;
      flex-direction: column;
      gap: 48px;
    }
  }
  &__controls {
    display: flex;
    justify-content: space-between;
  }
  &__total-items {
    display: none;
    font-size: 12px;
    font-weight: 500;
    line-height: 16px;
    text-transform: uppercase;
    letter-spacing: 0.06em;

    @media (min-width: 1024px) {
      display: block;
    }
  }
  &__filters-bottom-sheet {
    font-size: 12px;
    font-weight: 500;
    line-height: 16px;
    letter-spacing: 0.06em;
    background: none;
    border: none;
    padding: 0;
    margin: 0;
    text-transform: uppercase;

    @media (min-width: 1024px) {
      display: none;
    }
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

  &__carousel {
    display: none;
  }
  &__header {
    font-size: 36px;
    font-weight: 400;
    line-height: 31.68px;
  }
}
</style>
