<template lang="pug">
div(class="carousel")
  div(ref="container" v-bind="$attrs" class="keen-slider")
    slot
  div(v-if="slider && dotHelper > 1" class="dots")
    button(v-for="(_slide, idx) in dotHelper" :key="idx" :class="{ _active: current === idx }" @click="slider.moveToIdx(idx)")
  slot(name="arrows" v-bind="{ next, prev }")
</template>

<style lang="scss">
.carousel {
  position: relative;
  &__arrow-left {
    position: absolute;
    top: 50%;
    transform: translate(-50%);
    z-index: 1;
  }
}
.dots {
  display: inline-flex;
  justify-content: center;
  align-items: center;
  gap: 8px;
  background: rgba(0, 0, 0, 0.4);
  padding: 12px 24px;
  border-radius: 16px;
  position: absolute;
  bottom: 40px;
  left: 50%;
  transform: translateX(-50%);

  button {
    margin: 0;
    padding: 0;
    width: 6px;
    height: 6px;
    display: block;
    border-radius: 50%;
    background: #fff;
    opacity: 20%;
    border: none;
    transition: width 1s ease, height 1s ease, border-radius 1s ease;

    &._active {
      opacity: 1;
      transition: width 0.3s ease, height 0.3s ease, border-radius 0.3s ease;
    }
  }
}
</style>

<script setup>
import { computed, ref } from "vue";
import "keen-slider/keen-slider.min.css";
import { useKeenSlider } from "keen-slider/vue";

const props = defineProps({
  modelValue: {
    type: Number,
    default: 0,
  },
  autoAdjustSlidesPerView: {
    type: Boolean,
    default: false,
  },
  breakpoints: {
    type: Object,
    default: undefined,
  },
  centered: {
    type: Boolean,
    default: false,
  },
  controls: {
    type: Boolean,
    default: true,
  },
  dragSpeed: {
    type: Number,
    default: 1,
  },
  duration: {
    type: Number,
    default: 500,
  },
  loop: {
    type: Boolean,
    default: false,
  },
  mode: {
    type: String,
    default: "snap",
  },
  resetSlide: {
    type: Boolean,
    default: false,
  },
  rtl: {
    type: Boolean,
    default: false,
  },
  rubberband: {
    type: Boolean,
    default: true,
  },
  slidesPerView: {
    type: Number,
    default: 1,
  },
  spacing: {
    type: Number,
    default: 0,
  },
  vertical: {
    type: Boolean,
    default: false,
  },
  autoplay: {
    type: Boolean,
    default: false,
  },
  autoplayTimeout: {
    type: Number,
    default: 3000,
  },
  arrows: {
    type: Boolean,
    default: false,
  },
});

const options = computed(() => ({
  breakpoints: props.breakpoints,
}));

const currentSlidesPerView = ref(null);
const current = ref(0);
const [container, slider] = useKeenSlider({
  initial: current.value,
  slideChanged: (s) => {
    current.value = s.track.details.rel;
  },
  created: (e) => {
    console.log(e, "e");
    currentSlidesPerView.value = e.options.slides.perView;
  },
  updated: (e) => {
    currentSlidesPerView.value = e.options.slides.perView;
  },
  ...options.value,
});

const dotHelper = computed(() =>
  slider.value && slider.value?.track?.details?.slides?.length
    ? slider.value.track.details.slides.length - currentSlidesPerView.value + 1
    : 0
);

const next = () => {
  slider.value.next();
};
const prev = () => {
  slider.value.prev();
};
</script>
