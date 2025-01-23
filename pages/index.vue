<script setup>
import { ref, computed, onMounted } from 'vue';

const posts = ref([]);
const loading = ref(true);
const pageNumber = ref(1);
const postsPerPage = 6;

// Fetch posts
const fetchPosts = async () => {
  const res = await fetch('/posts.json'); // Fetching the static JSON
  posts.value = await res.json();
  loading.value = false;
};

// Calculate total pages based on the number of posts and posts per page
const totalPage = computed(() => Math.ceil(posts.value.length / postsPerPage));

// Paginated posts for the current page
  const paginatedPosts = computed(() => {
  const startIndex = (pageNumber.value - 1) * postsPerPage;
  const endIndex = startIndex + postsPerPage;
  return posts.value.slice(startIndex, endIndex);
});

// Handlers for pagination buttons
const onPreviousPageClick = () => {
  if (pageNumber.value > 1) pageNumber.value--;
};

const onNextPageClick = () => {
  if (pageNumber.value < totalPage.value) pageNumber.value++;
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
        v-for="post in paginatedPosts"
        :key="post.id"
        class="group border m-2 overflow-hidden rounded-2xl shadow-sm text-zinc-700 dark:text-gray-200 p-4"
      >
        <h3 class="text-xl font-semibold">{{ post.title }}</h3>
        <p>{{ post.excerpt }}</p>
        <NuxtLink
          :to="`/posts/${post.slug}`"
          class="text-blue-500 hover:underline mt-2 inline-block"
        >
          Read More
        </NuxtLink>
      </div>
    </div>

    <!-- Pagination  -->
    <div v-if="!loading" class="flex justify-center items-center space-x-6 mt-4">
      <button :disabled="pageNumber <= 1" @click="onPreviousPageClick">
        &#x2190;
      </button>
      <p>{{ pageNumber }} / {{ totalPage }}</p>
      <button :disabled="pageNumber >= totalPage" @click="onNextPageClick">
        &#x2192;
      </button>
    </div>
  </div>
</template>
