<script setup lang="ts">
import { navbarData } from '../../data'
import { useRoute } from 'vue-router'
import { ref } from 'vue'

// Modal visibility
const isModalOpen = ref(false);

// Form fields
const formData = ref({
  name: '',
  email: '',
  message: '',
});

// Validation errors
const errors = ref({
  name: '',
  email: '',
  message: '',
});

// Open/close modal functions
const openModal = () => {
  isModalOpen.value = true;
  document.addEventListener('keydown', handleKeydown);
};

const closeModal = () => {
  isModalOpen.value = false;
  document.removeEventListener('keydown', handleKeydown);
};

// Handle Esc key to close modal
const handleKeydown = (event) => {
  if (event.key === 'Escape') {
    closeModal();
  }
};

// Validation logic
const validateForm = () => {
  let isValid = true;

  // Name validation
  if (!formData.value.name.trim()) {
    errors.value.name = 'Name is required.';
    isValid = false;
  } else {
    errors.value.name = '';
  }

  // Email validation
  const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
  if (!formData.value.email.trim()) {
    errors.value.email = 'Email is required.';
    isValid = false;
  } else if (!emailRegex.test(formData.value.email)) {
    errors.value.email = 'Enter a valid email address.';
    isValid = false;
  } else {
    errors.value.email = '';
  }

  // Message validation
  if (!formData.value.message.trim()) {
    errors.value.message = 'Message is required.';
    isValid = false;
  } else {
    errors.value.message = '';
  }

  return isValid;
};

// Handle form submission
const handleSubmit = () => {
  if (validateForm()) {
    alert('Form submitted successfully!');
    closeModal();
  }
};
const route = useRoute()
</script>

<template>
  <div class="py-5 max-w-5xl border-b m-auto">
    <ul class="flex justify-between items-baseline space-x-5">
      <li class="text-base sm:text-2xl font-bold">
        <NuxtLink to="/" :class="{ underline: route.path === '/' }">
          {{ navbarData.homeTitle }}
        </NuxtLink>
      </li>
      <li class="text-base sm:text-xl font-bold cursor-pointer" @click="openModal">
        Contact
      </li>
    </ul>
  </div>
  <!-- Modal -->
  <div
    v-if="isModalOpen"
    class="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center z-50"
    @click.self="closeModal"
  >
    <div class="bg-white w-full max-w-md p-6 rounded shadow-lg relative">
      <!-- Close button -->
      <button
        @click="closeModal"
        class="absolute top-2 right-2 text-gray-500 hover:text-gray-700"
      >
        &times;
      </button>

      <h2 class="text-xl font-bold mb-4">Contact Us</h2>

      <!-- Form -->
      <form @submit.prevent="handleSubmit">
        <div class="mb-4">
          <label for="name" class="block text-sm font-medium">Name</label>
          <input
            id="name"
            v-model="formData.name"
            type="text"
            class="w-full border border-gray-300 rounded px-3 py-2"
          />
          <p v-if="errors.name" class="text-red-500 text-sm">{{ errors.name }}</p>
        </div>

        <div class="mb-4">
          <label for="email" class="block text-sm font-medium">Email</label>
          <input
            id="email"
            v-model="formData.email"
            type="email"
            class="w-full border border-gray-300 rounded px-3 py-2"
          />
          <p v-if="errors.email" class="text-red-500 text-sm">{{ errors.email }}</p>
        </div>

        <div class="mb-4">
          <label for="message" class="block text-sm font-medium">Message</label>
          <textarea
            id="message"
            v-model="formData.message"
            rows="4"
            class="w-full border border-gray-300 rounded px-3 py-2"
          ></textarea>
          <p v-if="errors.message" class="text-red-500 text-sm">{{ errors.message }}</p>
        </div>

        <div class="flex justify-end">
          <button type="button" @click="closeModal" class="px-4 py-2 mr-2 bg-gray-200 rounded">
            Cancel
          </button>
          <button type="submit" class="px-4 py-2 bg-blue-500 text-white rounded">
            Submit
          </button>
        </div>
      </form>
    </div>
  </div>
</template>
