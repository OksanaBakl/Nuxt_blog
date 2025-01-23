<script setup lang="ts">
import { navbarData } from '../../data'
import { useRoute } from 'vue-router'
import { useColorMode } from '@vueuse/core';
import Modal from '../Modal.vue';

const route = useRoute()

const colorMode = useColorMode();

</script>

<template>
  <div class="py-5 max-w-5xl border-b m-auto">
    <ul class="flex justify-between items-baseline space-x-5">
      <li class="text-base sm:text-2xl font-bold">
        <NuxtLink to="/" :class="{ underline: route.path === '/' }">
          {{ navbarData.homeTitle }}
        </NuxtLink>
      </li>
      <li>
        <Modal />
      </li>
      <li>

      </li>
    </ul>
  </div>
</template>
