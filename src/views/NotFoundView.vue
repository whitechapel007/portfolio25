<script setup lang="ts">
import { RouterLink } from 'vue-router'
import { onMounted } from 'vue'
import gsap from 'gsap'

onMounted(() => {
  // Animate elements
  gsap.from('.not-found-title', {
    opacity: 0,
    y: 30,
    duration: 0.8
  })
  
  gsap.from('.not-found-subtitle', {
    opacity: 0,
    y: 30,
    duration: 0.8,
    delay: 0.2
  })
  
  gsap.from('.not-found-cta', {
    opacity: 0,
    y: 30,
    duration: 0.8,
    delay: 0.4
  })
})
</script>

<template>
  <div class="min-h-[80vh] flex items-center justify-center bg-white dark:bg-gray-900">
    <div class="text-center px-4 sm:px-6 lg:px-8">
      <h1 class="not-found-title text-9xl font-bold text-primary-600">404</h1>
      <p class="not-found-subtitle mt-4 text-3xl font-semibold text-gray-900 dark:text-white">
        Page Not Found
      </p>
      <p class="mt-6 text-base text-gray-600 dark:text-gray-400">
        Sorry, the page you are looking for doesn't exist or has been moved.
      </p>
      <div class="not-found-cta mt-10">
        <RouterLink to="/" class="btn btn-primary">
          Back to Home
        </RouterLink>
      </div>
    </div>
  </div>
</template>
