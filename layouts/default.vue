<script setup lang="ts">
import MainHeader from '../components/main/header.vue'
import MainFooter from '../components/main/footer.vue'
</script>

<template>
    <div class="gd-container font-spacegrotesk">
      <header class="p-4">
        <MainHeader />
      </header>
      <main class="max-w-5xl mx-auto">
        <slot />
      </main>
      <footer>
        <MainFooter />
      </footer>
    </div>
  </template>

  <style scoped>
  .gd-container {
    display: grid;
    grid-template-rows: auto 1fr auto;
    min-height: 100vh;
  }
  </style>
