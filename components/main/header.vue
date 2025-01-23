<script setup lang="ts">
import { navbarData } from '../../data'
import { useRoute } from 'vue-router'
import { useColorMode } from '@vueuse/core';
import Modal from '../Modal.vue';

const route = useRoute()

const colorMode = useColorMode();
// Toggle color mode function
const toggleColorMode = () => {
  colorMode.value = colorMode.value === 'dark' ? 'light' : 'dark';
};
</script>

<template>
  <div class="py-5 max-w-5xl border-b m-auto">
    <ul class="flex justify-between items-baseline space-x-5">
      <li class="text-base sm:text-2xl font-bold">
        <NuxtLink to="/" :class="{ underline: route.path === '/' }">
          {{ navbarData.homeTitle }}
        </NuxtLink>
      </li>
      <li class="flex items-baseline">
        <Modal />
        <!-- Color Mode Toggle Button -->
        <button
          @click="toggleColorMode"
          class="ml-3 px-4 py-2 rounded bg-gray-800 text-gray-200 dark:bg-[#F1F1F1] dark:text-gray-500 transition-colors"
        >
          {{ colorMode === 'dark' ? 'Light Mode' : 'Dark Mode' }}
        </button>
      </li>
    </ul>
  </div>
</template>
