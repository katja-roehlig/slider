<script setup>
import Carousel from './components/carousel/Carousel.vue'
const slides = [
  'https://picsum.photos/id/1032/900/400',
  'https://picsum.photos/id/1038/900/400',
  'https://picsum.photos/id/1037/900/400',
  'https://picsum.photos/id/1035/900/400',
  'https://picsum.photos/id/1036/900/400',
  'https://picsum.photos/id/1040/900/400',
  'https://picsum.photos/id/1039/900/400',
  'https://picsum.photos/id/1041/900/400',
  'https://picsum.photos/id/1042/900/400',
  'https://picsum.photos/id/1043/900/400'
]
</script>

<template>
  <Carousel :slides="slides" :interval="6000" controls indicators />
</template>

<style scoped></style>
