<script setup>
import { ref, onMounted, onBeforeUnmount } from 'vue'
import CarouselItem from './CarouselItem.vue'

const props = defineProps({ slides: Object })
console.log(props.slides)
let currentSlide = ref(0)
let slideInterval = ref(null)

onMounted(() => {
  slideInterval = setInterval(() => {
    const index = currentSlide.value < props.slides.length - 1 ? currentSlide.value + 1 : 0
    /* let index = 0
    if (currentSlide.value < props.slides.length - 1) {
      index = currentSlide.value + 1
    } else {
      index = 0
    } */
    setCurrentSlide(index)
  }, 3000)
})
console.log(slideInterval)

onBeforeUnmount(() => {
  clearInterval(slideInterval)
})

function setCurrentSlide(index) {
  currentSlide.value = index
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
