<script setup>
const props = defineProps({ slide: String, currentSlide: Number, index: Number })
</script>

<template>
  <transition name="slide-in">
    <div class="carousel-item" v-show="props.currentSlide === props.index">
      <img :src="props.slide" />
    </div>
  </transition>
</template>

<style scoped>
.carousel-item {
  position: absolute;
  left: 0;
  right: 0;
  top: 0;
  bottom: 0;
}
.slide-in-enter-active,
.slide-in-leave-active {
  transition: all 1s ease-in-out;
}
.slide-in-enter-from {
  transform: translateX(-100%);
}
.slide-in-leave-to {
  transform: translateX(100%);
}
</style>
