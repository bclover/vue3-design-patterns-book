<script setup lang="ts">
import HelloWorld from './components/HelloWorld.vue';
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
  padding: 1.5rem;
  will-change: filter;
  transition: filter 300ms;
}
.logo {
  height: 6rem;
  padding: 1.5rem;
  will-change: filter;
  transition: filter 300ms;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
