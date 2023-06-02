<script setup>
const props = defineProps({ slide: String })
</script>

<template>
  <div class="carousel-item">
    <img :src="slide" />
  </div>
</template>
