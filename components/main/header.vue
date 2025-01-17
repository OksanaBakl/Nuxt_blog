<script setup lang="ts">
import { navbarData } from '../../data'
import { useRoute } from 'vue-router'

const route = useRoute()
</script>

<template>
  <div class="py-5 max-w-5xl border-b flex justify-center m-auto">
    <ul>
      <li class="text-base sm:text-2xl font-bold">
        <NuxtLink to="/" :class="{ underline: route.path === '/' }">
          {{ navbarData.homeTitle }}
        </NuxtLink>
      </li>
    </ul>
  </div>
</template>
