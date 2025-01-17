<script setup lang="ts">
import { navbarData } from '../../data'
import { useRoute } from 'vue-router'
import { ref } from 'vue'
import Modal from '../Modal.vue';


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
      <li>
        <Modal />
      </li>
    </ul>
  </div>
</template>
