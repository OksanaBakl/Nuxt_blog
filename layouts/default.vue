<script setup lang="ts">
import { navbarData } from '../data'

const route = useRoute()
function isActive(path: string) {
  return route.path.startsWith(path)
}
</script>

<template>
    <div class="gd-container font-spacegrotesk">
      <header class="p-4">
        <div class="flex py-5 max-w-5xl border-b dark:border-gray-800 justify-center mx-auto items-baseline">
          <ul class="flex items-baseline space-x-5">
            <li class="text-base sm:text-2xl font-bold">
              <NuxtLink to="/" :class="{ underline: $route.path === '/' }">
                {{ navbarData.homeTitle }}
              </NuxtLink>
            </li>
          </ul>
        </div>
    </header>
      <main class="max-w-5xl mx-auto">
        <slot />
      </main>
      <footer class="max-w-5xl mx-auto py-5 flex justify-between">
        MainFooter
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