<template lang="pug">
div(v-bind="$attrs" class="keen-slider__slide")
  slot
</template>

<style lang="scss" scoped>
.keen-slider__slide {
  overflow: visible !important;
}
</style>
