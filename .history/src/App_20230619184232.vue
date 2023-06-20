<script setup lang="ts">
import HelloWorld from './components/ToDos.vue';
</script>

<template>
  <div>
    <a href="https://vitejs.dev" target="_blank">
      <img src="/vite.svg" class="logo" alt="Vite logo" />
    </a>
    <a href="https://vuejs.org/" target="_blank">
      <i class="fa-brands fa-vuejs fa-3x vue-green"></i>
    </a>
  </div>
  <HelloWorld msg="Vite + Vue" />
</template>

<style scoped>
.vue-green {
  color: green;
  margin-top: 1rem;
  will-change: filter;
  transition: filter 300ms;
}
</style>
