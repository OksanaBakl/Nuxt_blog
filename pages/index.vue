<script setup>
import { ref, onMounted } from 'vue';

const posts = ref([]);
const loading = ref(true);

const fetchPosts = async () => {
  const res = await fetch('/posts.json'); // Fetching the static JSON
  posts.value = await res.json();
  loading.value = false;
};

onMounted(() => {
  fetchPosts();
});
</script>

<template>
  <div>
    <h2 class="text-3xl font-bold my-6 text-center">Posts</h2>

    <div v-if="loading" class="text-gray-500">Loading...</div>
    <div v-else class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3">
      <div
        v-for="post in posts"
        :key="post.id"
        class="group border m-2 overflow-hidden rounded-2xl shadow-sm text-zinc-700 p-4"
      >
        <h3 class="text-xl font-semibold">{{ post.title }}</h3>
        <p class="text-gray-700">{{ post.excerpt }}</p>
        <NuxtLink
          :to="`/posts/${post.slug}`"
          class="text-blue-500 hover:underline mt-2 inline-block"
        >
          Read More
        </NuxtLink>
      </div>
    </div>
  </div>
</template>
