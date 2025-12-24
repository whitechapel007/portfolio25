<!-- eslint-disable vue/multi-word-component-names -->
<script setup lang="ts">
import { onMounted, onUnmounted, ref } from 'vue'
import { RouterLink } from 'vue-router'
import gsap from 'gsap'
import Button from './ui/Button.vue'

const isScrolled = ref(false)
const isMobileMenuOpen = ref(false)

const navLinks = [
  { name: 'Home', path: '/' },
  { name: 'About', path: '/about' },
  { name: 'Skills', path: '/skills' },
  { name: 'Projects', path: '/projects' },
  { name: 'Experience', path: '/experience' },
  { name: 'Contact', path: '/contact' },
]

const handleScroll = () => {
  isScrolled.value = window.scrollY > 50
}

const closeMobileMenu = () => {
  isMobileMenuOpen.value = false
}

const toggleMobileMenu = () => {
  isMobileMenuOpen.value = !isMobileMenuOpen.value

  // Animate mobile menu
  if (isMobileMenuOpen.value) {
    gsap.from('.mobile-menu', {
      opacity: 0,
      y: -20,
      duration: 0.3,
      ease: 'power2.out',
    })
  }
}

onMounted(() => {
  window.addEventListener('scroll', handleScroll)

  // Initial navbar animation
  gsap.from('.navbar-brand', {
    opacity: 0,
    y: -20,
    duration: 0.6,
    delay: 0.2,
  })

  gsap.from('.navbar-links', {
    opacity: 0,
    y: -20,
    duration: 0.6,
    delay: 0.4,
  })

  gsap.from('.navbar-button', {
    opacity: 0,
    scale: 0.8,
    duration: 0.6,
    delay: 0.6,
  })
})

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll)
})
</script>

<template>
  <nav
    class="fixed top-0 left-0 w-full z-50 transition-all duration-300"
    :class="{
      'bg-white/80 dark:bg-gray-900/80 backdrop-blur-md shadow-md': isScrolled,
      'bg-transparent': !isScrolled,
    }"
  >
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
      <div class="flex justify-between h-16">
        <div class="flex items-center">
          <RouterLink to="/" class="navbar-brand flex-shrink-0 flex items-center">
            <span
              class="text-xl font-bold text-white hover:text-cyan-400 transition-colors duration-300"
              >Ebuka</span
            >
          </RouterLink>
        </div>

        <!-- Desktop menu -->
        <div class="navbar-links hidden md:flex items-center space-x-8">
          <div class="flex space-x-6">
            <RouterLink
              v-for="link in navLinks"
              :key="link.name"
              :to="link.path"
              class="text-gray-300 hover:text-cyan-400 px-3 py-2 text-sm font-medium transition-colors duration-300 relative group"
              active-class="text-cyan-400"
            >
              {{ link.name }}
              <span
                class="absolute bottom-0 left-0 w-0 h-0.5 bg-cyan-400 transition-all duration-300 group-hover:w-full"
              ></span>
            </RouterLink>
          </div>

          <Button variant="outline" size="sm" class="navbar-button">Resume</Button>
        </div>

        <!-- Mobile menu button -->
        <div class="flex items-center md:hidden">
          <button
            @click="toggleMobileMenu"
            class="inline-flex items-center justify-center p-2 rounded-md text-gray-700 dark:text-gray-300 hover:text-primary-600 dark:hover:text-primary-500 focus:outline-none"
          >
            <svg
              class="h-6 w-6"
              xmlns="http://www.w3.org/2000/svg"
              fill="none"
              viewBox="0 0 24 24"
              stroke="currentColor"
            >
              <path
                v-if="!isMobileMenuOpen"
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="2"
                d="M4 6h16M4 12h16M4 18h16"
              />
              <path
                v-else
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="2"
                d="M6 18L18 6M6 6l12 12"
              />
            </svg>
          </button>
        </div>
      </div>
    </div>

    <!-- Mobile menu -->
    <div
      v-if="isMobileMenuOpen"
      class="mobile-menu md:hidden bg-gray-900 shadow-lg border-t border-gray-800"
    >
      <div class="px-4 pt-4 pb-6 space-y-2">
        <RouterLink
          v-for="link in navLinks"
          :key="link.name"
          :to="link.path"
          class="block px-4 py-3 rounded-lg text-base font-medium text-gray-300 hover:text-cyan-400 hover:bg-gray-800 transition-colors duration-300"
          active-class="text-cyan-400 bg-gray-800"
          @click="closeMobileMenu"
        >
          {{ link.name }}
        </RouterLink>

        <div class="pt-4 border-t border-gray-700">
          <Button variant="primary" full-width @click="closeMobileMenu">Resume</Button>
        </div>
      </div>
    </div>
  </nav>
</template>
