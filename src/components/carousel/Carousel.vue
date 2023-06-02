<script setup>
import CarouselItem from './CarouselItem.vue'
const props = defineProps({ slides: Object })
</script>

<template>
  <div class="carousel">
    <div class="carousel-inner">
      <CarouselItem v-for="(slide, index) in slides" :slide="slide" :key="`item-${index}`" />
    </div>
  </div>
</template>
