<script setup lang="ts">
import { Bars3Icon, XMarkIcon } from '@heroicons/vue/24/outline'
import { onMounted, ref, watch } from 'vue'
import { RouterLink, useRoute } from 'vue-router'

const route = useRoute()
const isMenuOpen = ref(false)
const isScrolled = ref(false)

const toggleMenu = () => {
  isMenuOpen.value = !isMenuOpen.value
}

const closeMenu = () => {
  isMenuOpen.value = false
}

const handleScroll = () => {
  isScrolled.value = window.scrollY > 50
}

onMounted(() => {
  window.addEventListener('scroll', handleScroll)
})

watch(() => route.path, () => {
  closeMenu()
})

const navLinks = [
  { name: 'HOME', path: '/' },
  { name: 'ABOUT', path: '/about' },
  { name: 'WORK', path: '/projects' },
  { name: 'SKILLS', path: '/skills' },
  { name: 'CONTACT', path: '/contact' }
]
</script>

<template>
  <header class="fixed top-0 left-0 w-full z-50 transition-all duration-300"
    :class="{ 'py-4 bg-black/80 backdrop-blur-md': isScrolled, 'py-6': !isScrolled }">
    <div class="container mx-auto px-6 flex justify-between items-center">
      <!-- Logo -->
      <RouterLink to="/" class="text-2xl font-bold tracking-wider">
        <span class="text-white">EBUKA</span>
        <span class="text-[#00E0FF]">.</span>
      </RouterLink>

      <!-- Desktop Navigation -->
      <nav class="hidden md:block">
        <ul class="flex space-x-8">
          <li v-for="link in navLinks" :key="link.path">
            <RouterLink :to="link.path"
              class="text-sm tracking-widest hover:text-[#00E0FF] transition-colors duration-300"
              :class="route.path === link.path ? 'text-[#00E0FF]' : 'text-white'">
              {{ link.name }}
            </RouterLink>
          </li>
        </ul>
      </nav>

      <!-- Mobile Menu Button -->
      <button @click="toggleMenu" class="md:hidden text-white focus:outline-none" aria-label="Toggle menu">
        <Bars3Icon v-if="!isMenuOpen" class="h-6 w-6" />
        <XMarkIcon v-else class="h-6 w-6" />
      </button>
    </div>

    <!-- Mobile Menu -->
    <div v-if="isMenuOpen" class="md:hidden fixed inset-0 bg-black z-40 flex flex-col justify-center items-center">
      <nav>
        <ul class="flex flex-col space-y-8 items-center">
          <li v-for="link in navLinks" :key="link.path">
            <RouterLink :to="link.path"
              class="text-xl tracking-widest hover:text-[#00E0FF] transition-colors duration-300"
              :class="route.path === link.path ? 'text-[#00E0FF]' : 'text-white'" @click="closeMenu">
              {{ link.name }}
            </RouterLink>
          </li>
        </ul>
      </nav>
    </div>
  </header>
</template>
