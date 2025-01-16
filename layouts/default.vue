<script setup lang="ts">
import { navbarData } from '../data'

const route = useRoute()
function isActive(path: string) {
  return route.path.startsWith(path)
}
</script>

<template>
    <!-- <div class="gd-container font-spacegrotesk"> -->
      <header class="bg-blue-600 text-white p-4">
        <div class="py-5 border-b dark:border-gray-800 font-semibold">
        <div class="flex px-6 container max-w-5xl justify-between mx-auto items-baseline">
          <ul class="flex items-baseline space-x-5">
            <li class="text-base sm:text-2xl font-bold">
              <NuxtLink to="/" :class="{ underline: $route.path === '/' }">
                {{ navbarData.homeTitle }}
              </NuxtLink>
            </li>
          </ul>
          <ul class="flex items-center space-x-3 sm:space-x-6 text-sm sm:text-lg">
            <li>
              <NuxtLink to="/blogs" :class="{ underline: isActive('/blogs') }"> Blogs </NuxtLink>
            </li>
            <li>
              <NuxtLink to="/categories" :class="{ underline: isActive('/categories') }">
                Categories
              </NuxtLink>
            </li>
            <li title="About Me">
              <NuxtLink
                to="/about"
                aria-label="About me"
                :class="{ underline: $route.path === '/about' }"
              >
                About
              </NuxtLink>
            </li>
          </ul>
        </div>
      </div>
    </header>
      <main>
        <div class="p-9" />
        <slot />
      </main>
      <footer>
        MainFooter
      </footer>
    <!-- </div> -->
  </template>
  
  <style scoped>
  .gd-container {
    display: grid;
    /* grid-template-rows: 1fr auto; */
    min-height: 100vh;
  }
  </style>