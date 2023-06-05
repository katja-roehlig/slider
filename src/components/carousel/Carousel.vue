<script setup>
import { ref, onMounted, onBeforeUnmount } from 'vue'
import CarouselItem from './CarouselItem.vue'
import CarouselControls from './CarouselControls.vue'
import CarouselIndicators from './CarouselIndicators.vue'

const props = defineProps({
  slides: { type: Array, required: true },
  controls: { type: Boolean, default: false },
  indicators: { type: Boolean, default: false },
  interval: { type: Number, default: 5000 }
})
let currentSlide = ref(0)
let slideInterval = ref(null)
let direction = 'right'

onMounted(() => {
  startSlideTimer()
})

onBeforeUnmount(() => {
  stopSlideTimer()
})

function startSlideTimer() {
  stopSlideTimer()
  slideInterval = setInterval(() => {
    nextFirst()
  }, props.interval)
}

function stopSlideTimer() {
  clearInterval(slideInterval)
}
function setCurrentSlide(index) {
  currentSlide.value = index
}

function prev(step = -1) {
  const index = currentSlide.value > 0 ? currentSlide.value + step : props.slides.length - 1
  setCurrentSlide(index)
  direction = 'left'
  startSlideTimer()
}
function nextFirst(step = 1) {
  const index = currentSlide.value < props.slides.length - 1 ? currentSlide.value + step : 0
  setCurrentSlide(index)
  direction = 'right'
}
function next(step) {
  nextFirst(step)
  startSlideTimer()
  /*if (currentSlide.value < props.slides.length - 1) {
      index = currentSlide.value + 1
    } else {
      index = 0
    } */
}
function switchSlide(index) {
  const step = index - currentSlide.value
  if (step > 0) {
    next(step)
  } else {
    prev(step)
  }
}
</script>

<template>
  <div class="carousel">
    <div class="carousel-inner">
      <CarouselItem
        v-for="(slide, index) in slides"
        :slide="slide"
        :key="`item-${index}`"
        :current-slide="currentSlide"
        :index="index"
        :direction="direction"
        @mouseenter="stopSlideTimer"
        @mouseout="startSlideTimer"
      />
      <CarouselControls v-if="controls" @prev="prev" @next="next" />
      <CarouselIndicators
        v-if="indicators"
        :total="slides.length"
        :current-index="currentSlide"
        @switch="switchSlide($event)"
      />
    </div>
  </div>
</template>
<style scoped>
.carousel {
  display: flex;
  justify-content: center;
}
.carousel-inner {
  position: relative;
  width: 900px;
  height: 400px;
  overflow: hidden;
}
</style>
