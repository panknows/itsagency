<template lang="pug">
div(class="header", :class="isMenuOpen && '_open'")
  div(class="container header__container")
    div(class="header__wrapper")
      button(class="header__burger" @click="isMenuOpen = !isMenuOpen")
        img(:src="BurgerIcon")
      div(class="header__logo")
        img(:src="Logo")
      div(class="header__content")
        ul(class="header__list")
          li(v-for="(link, i) in ['Продукты', 'Цвета', 'Вдохновение', 'Советы', 'Найти магазин']", :key="i", class="header__list-item")
            a(href="/", class="header__link") {{ link }}
        a(href="tel:+7 (495) 221-77-69", class="header__call")
          p +7 (495) 221-77-69
          span Заказать звонок
        div(class="header__nav")
          button(v-for="(nav, i) in navs", :key="i", class="header__nav-item")
            img(:src="nav.iconPath")

      a(href="/", class="avatar header__avatar")
        span 4
</template>

<script setup lang="ts">
import Logo from "@/shared/assets/images/logo.png";
import BurgerIcon from "@/shared/assets/icons/burger.svg";
import SearchIcon from "@/shared/assets/icons/search.svg";
import ProfileIcon from "@/shared/assets/icons/profile.svg";
import HeartIcon from "@/shared/assets/icons/heart.svg";
import { ref } from "vue";

const navs = [
  {
    iconPath: SearchIcon,
  },
  {
    iconPath: ProfileIcon,
  },
  {
    iconPath: HeartIcon,
  },
];

const isMenuOpen = ref(false);
</script>

<style lang="scss">
.header {
  $root: &;

  background: #fff;

  &._open {
    #{$root}__content {
      display: flex;
    }
  }

  &__wrapper {
    display: flex;
    justify-content: space-between;
    align-items: center;
    flex-wrap: wrap;
    padding: 20px 0;
    box-sizing: border-box;
    height: 64px;
    position: relative;
    border-bottom: 1px solid #1f20200f;

    @media (min-width: 1024px) {
      flex-wrap: nowrap;
      height: 104px;
      border-bottom: 0;
    }
  }

  &__burger {
    background: none;
    border: none;
    margin: 0;
    padding: 0;

    @media (min-width: 1024px) {
      display: none;
    }

    img {
    }
  }

  &__logo {
    position: absolute;
    left: 50%;
    transform: translateX(-50%);

    @media (min-width: 1024px) {
      position: static;
      transform: none;
    }

    img {
    }
  }

  &__content {
    flex-basis: 100%;
    order: 1;
    position: absolute;
    align-self: flex-start;
    display: none;
    flex-direction: column;
    align-items: center;
    gap: 32px;
    top: 100%;
    left: 0;
    width: 100%;
    padding-top: 24px;
    background: #fff;

    @media (min-width: 1024px) {
      display: flex;
      position: static;
      order: 0;
      flex-direction: row;
      padding-top: 0;
      align-self: center;
      padding-right: 24px;
      padding-left: 24px;
      gap: 24px;
    }
    @media (min-width: 1200px) {
      padding-left: 5%;
      gap: 5%;
    }
    @media (min-width: 1366px) {
      padding-left: 10%;
      gap: 8%;
    }
  }

  &__list {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 16px;

    @media (min-width: 1024px) {
      flex-direction: row;
    }
    @media (min-width: 1200px) {
      gap: 24px;
    }

    &-item {
      display: flex;
    }
  }

  &__link {
    font-size: 14px;
    font-weight: 400;
    line-height: 14px;
    text-decoration: none;
    color: #1f2020;
    text-transform: uppercase;
  }

  &__call {
    text-decoration: none;
    display: flex;
    flex-direction: column;

    @media (min-width: 1024px) {
      margin-left: auto;
    }

    p {
      font-size: 16px;
      font-weight: 500;
      line-height: 16px;
      color: #1f2020;
      margin-bottom: 2px;
    }
    span {
      font-size: 14px;
      font-weight: 400;
      line-height: 14px;
      color: #1f20204d;
    }
  }

  &__nav {
    order: -1;
    display: flex;
    align-items: center;
    gap: 24px;

    @media (min-width: 1024px) {
      order: 1;
    }

    &-item {
      background: none;
      border: none;
      margin: 0;
      padding: 0;
      display: flex;
      align-items: center;

      img {
        width: 22px;
      }
    }
  }
}

.avatar {
  width: 24px;
  min-width: 24px;
  height: 24px;
  border-radius: 50%;
  background: #7bb899;
  display: flex;
  align-items: center;
  justify-content: center;
  text-decoration: none;

  span {
    font-size: 12px;
    font-weight: 500;
    text-align: center;
  }
}
</style>
