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
    <div v-if="loading" class="text-gray-500">Loading...</div>
    <div v-else-if="post">
      <h2 class="text-3xl font-bold mb-4">{{ post.title }}</h2>
      <p class="text-gray-700">{{ post.content }}</p>
    </div>
    <div v-else class="text-red-500">Post not found!</div>
  </div>
</template>
