<script setup>
import { ref, onMounted, onBeforeUnmount } from 'vue'
import CarouselItem from './CarouselItem.vue'
import CarouselControls from './CarouselControls.vue'

const props = defineProps({ slides: Object })
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
  }, 5000)
}

function stopSlideTimer() {
  clearInterval(slideInterval)
}
function setCurrentSlide(index) {
  currentSlide.value = index
}

function prev() {
  const index = currentSlide.value > 0 ? currentSlide.value - 1 : props.slides.length - 1
  setCurrentSlide(index)
  direction = 'left'
  startSlideTimer()
}
function nextFirst() {
  const index = currentSlide.value < props.slides.length - 1 ? currentSlide.value + 1 : 0
  setCurrentSlide(index)
  direction = 'right'
}
function next() {
  nextFirst()
  startSlideTimer()
  /*if (currentSlide.value < props.slides.length - 1) {
      index = currentSlide.value + 1
    } else {
      index = 0
    } */
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
      <CarouselControls @prev="prev" @next="next" />
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
