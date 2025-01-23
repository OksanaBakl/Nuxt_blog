<script setup>
import { ref, onMounted } from 'vue';
import { useRoute } from 'vue-router';

const route = useRoute();
const post = ref(null);
const loading = ref(true);

const fetchPost = async () => {
  const res = await fetch('/posts.json');
  const posts = await res.json();
  post.value = posts.find((p) => p.slug === route.params.slug);
  loading.value = false;
};

onMounted(() => {
  fetchPost();
});
</script>

<template>
  <div>
    <div v-if="loading" class="text-gray-500 dark:text-gray-200">Loading...</div>
    <div v-else-if="post" class="px-4 text-gray-700 dark:text-gray-200">
      <h2 class="text-3xl font-bold mb-4">{{ post.title }}</h2>
      <p>{{ post.content }}</p>
      <NuxtLink to="/" class="text-blue-500 hover:underline mt-2 inline-block">Back to all Posts</NuxtLink>
    </div>
    <div v-else class="text-red-500">Post not found!</div>
  </div>
</template>
