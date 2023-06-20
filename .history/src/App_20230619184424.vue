<script setup lang="ts">
import ToDos from '@components/ToDos.vue';
</script>

<template>
  <div class="app w3-blue-gray">
    <ToDos />
  </div>
</template>

<style scoped>
.vue-green {
  color: green;
  margin-top: 1rem;
  will-change: filter;
  transition: filter 300ms;
}
</style>
