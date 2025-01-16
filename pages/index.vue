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
    <h2 class="text-3xl font-bold mb-6">Blog Posts</h2>

    <div v-if="loading" class="text-gray-500">Loading...</div>
    <div v-else class="space-y-6">
      <div
        v-for="post in posts"
        :key="post.id"
        class="border p-4 rounded shadow"
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
