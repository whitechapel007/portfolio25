<!-- eslint-disable vue/multi-word-component-names -->
<script setup lang="ts">
import { onMounted, onUnmounted, ref } from 'vue'
import { RouterLink } from 'vue-router'

const isScrolled = ref(false)
const isMobileMenuOpen = ref(false)

const navLinks = [
  { name: 'Home', path: '/' },
  { name: 'About', path: '/about' },
  { name: 'Skills', path: '/skills' },
  { name: 'Projects', path: '/projects' },
  { name: 'Experience', path: '/experience' },
  { name: 'Contact', path: '/contact' }
]

const handleScroll = () => {
  isScrolled.value = window.scrollY > 50
}

onMounted(() => {
  window.addEventListener('scroll', handleScroll)
})

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll)
})

const toggleMobileMenu = () => {
  isMobileMenuOpen.value = !isMobileMenuOpen.value
}
</script>

<template>
  <nav class="fixed top-0 left-0 w-full z-50 transition-all duration-300"
    :class="{ 'bg-white/80 dark:bg-gray-900/80 backdrop-blur-md shadow-md': isScrolled, 'bg-transparent': !isScrolled }">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
      <div class="flex justify-between h-16">
        <div class="flex items-center">
          <RouterLink to="/" class="flex-shrink-0 flex items-center">
            <span class="text-xl font-bold text-primary-600">Ebuka</span>
          </RouterLink>
        </div>

        <!-- Desktop menu -->
        <div class="hidden md:flex items-center space-x-8">
          <div class="flex space-x-6">
            <RouterLink v-for="link in navLinks" :key="link.name" :to="link.path"
              class="text-gray-700 dark:text-gray-300 hover:text-primary-600 dark:hover:text-primary-500 px-3 py-2 text-sm font-medium"
              active-class="text-primary-600 dark:text-primary-500">
              {{ link.name }}
            </RouterLink>
          </div>

          <button class="btn btn-primary">Resume</button>
        </div>

        <!-- Mobile menu button -->
        <div class="flex items-center md:hidden">
          <button @click="toggleMobileMenu"
            class="inline-flex items-center justify-center p-2 rounded-md text-gray-700 dark:text-gray-300 hover:text-primary-600 dark:hover:text-primary-500 focus:outline-none">
            <svg class="h-6 w-6" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24"
              stroke="currentColor">
              <path v-if="!isMobileMenuOpen" stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                d="M4 6h16M4 12h16M4 18h16" />
              <path v-else stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
            </svg>
          </button>
        </div>
      </div>
    </div>

    <!-- Mobile menu -->
    <div v-if="isMobileMenuOpen" class="md:hidden bg-white dark:bg-gray-900 shadow-lg">
      <div class="px-2 pt-2 pb-3 space-y-1">
        <RouterLink v-for="link in navLinks" :key="link.name" :to="link.path"
          class="block px-3 py-2 rounded-md text-base font-medium text-gray-700 dark:text-gray-300 hover:text-primary-600 dark:hover:text-primary-500"
          active-class="text-primary-600 dark:text-primary-500" @click="isMobileMenuOpen = false">
          {{ link.name }}
        </RouterLink>

        <button class="mt-4 w-full btn btn-primary">Resume</button>
      </div>
    </div>
  </nav>
</template>
