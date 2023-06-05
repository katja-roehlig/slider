<script setup>
const emit = defineEmits(['prev', 'next'])
</script>

<template>
  <button class="carousel-control left" @click="$emit('prev')">Prev</button>
  <button class="carousel-control right" @click="$emit('next')">Next</button>
</template>
<style scoped>
.carousel-control {
  background-color: rgba(0, 0, 0, 0.5);
  color: #f3f3f3;
  border: none;
  --display: inline-block;
  position: absolute;
  top: calc(50% - 25px);
  height: 50px;
  width: 70px;
  cursor: pointer;
}
.left {
  left: 0%;
}
.right {
  right: 0%;
}
</style>
