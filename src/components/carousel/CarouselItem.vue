<script setup>
import { computed } from 'vue'
const props = defineProps({ slide: String, currentSlide: Number, index: Number, direction: String })
const emit = defineEmits(['mouseenter', 'mouseout'])
const transitionEffect = computed(() => {
  return props.direction === 'right' ? 'slide-out' : 'slide-in'
})
</script>

<template>
  <transition :name="transitionEffect">
    <div
      class="carousel-item"
      v-show="props.currentSlide === props.index"
      @mouseenter="$emit('mouseenter')"
      @mouseout="$emit('mouseout')"
    >
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
.slide-in-leave-active,
.slide-out-enter-active,
.slide-out-leave-active {
  transition: all 1s ease-in-out;
}
.slide-in-enter-from {
  transform: translateX(-100%);
}
.slide-in-leave-to {
  transform: translateX(100%);
}
.slide-out-enter-from {
  transform: translateX(100%);
}
.slide-out-leave-to {
  transform: translateX(-100%);
}
</style>
