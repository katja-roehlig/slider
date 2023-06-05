<script setup>
const props = defineProps({ slide: String, currentSlide: Number, index: Number })
</script>

<template>
  <div class="carousel-item" v-show="props.currentSlide === props.index">
    <img :src="props.slide" />
  </div>
</template>

<style scoped>
.carousel-item {
  position: absolute;
  left: 0;
  right: 0;
  top: 0;
  bottom: 0;
}
</style>
