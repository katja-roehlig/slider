<script setup>
const props = defineProps({ total: Number, currentIndex: Number })
const emit = defineEmits(['switch'])
</script>

<template>
  <div class="carousel-indicators">
    <button
      class="carousel-indicator-item"
      :class="{ active: currentIndex === index }"
      v-for="(item, index) in props.total"
      :key="index"
      @click="$emit('switch', index)"
    ></button>
  </div>
</template>

<style scoped>
.carousel-indicators {
  position: absolute;
  left: 50%;
  bottom: 5%;
  transform: translateX(-50%);
}
.carousel-indicator-item {
  width: 0.8rem;
  height: 0.8rem;
  padding: 0;
  border: none;
  border-radius: 5rem;
  background-color: #ffffff;
  opacity: 0.5;
  cursor: pointer;
  margin-inline: 0.2rem;
}
.active {
  opacity: 1;
}
</style>
