<template>
  <nav class="breadcrumbs">
    <ul class="breadcrumbs__list">
      <li
        v-for="(breadcrumb, index) in breadcrumbs"
        :key="index"
        class="breadcrumbs__item"
      >
        <template v-if="index < breadcrumbs.length - 1">
          <a :href="breadcrumb.url" class="breadcrumbs__link">
            {{ breadcrumb.label }}
          </a>
          <span class="breadcrumbs__separator">·</span>
        </template>
        <span v-else class="breadcrumbs__active">{{ breadcrumb.label }}</span>
      </li>
    </ul>
  </nav>
</template>

<script lang="ts" setup>
import { defineProps } from "vue";

interface Breadcrumb {
  label: string;
  url?: string;
}

const props = defineProps<{
  breadcrumbs: Breadcrumb[];
}>();
</script>

<style lang="scss" scoped>
.breadcrumbs {
  display: flex;
  align-items: center;

  &__list {
    list-style: none;
    padding: 0;
    margin: 0;
    display: flex;
  }

  &__link {
    text-decoration: none;
    text-transform: uppercase;
    font-size: 10px;
    font-weight: 400;
    line-height: 10px;
    letter-spacing: 0.06em;
    color: #1f20204d;

    &:hover {
      text-decoration: underline;
    }
  }

  &__item {
    display: flex;
    align-items: center;
  }

  &__separator {
    margin: 0 3.5px;
    color: #1f20204d;
    font-weight: 700;
  }

  &__active {
    text-transform: uppercase;
    font-size: 10px;
    font-weight: 400;
    line-height: 10px;
    letter-spacing: 0.06em;
    color: #1f20204d;
  }
}
</style>
