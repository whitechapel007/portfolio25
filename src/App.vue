<script setup lang="ts">
import { onMounted, ref } from 'vue'
import { RouterView } from 'vue-router'
import MainFooter from './components/MainFooter.vue'
import MainNavigation from './components/MainNavigation.vue'

const appReady = ref(false)

onMounted(() => {
  // Simulate loading
  setTimeout(() => {
    appReady.value = true
  }, 500)
})
</script>

<template>
  <div class="min-h-screen flex flex-col bg-black text-white">
    <!-- Loading screen -->
    <div v-if="!appReady" class="fixed inset-0 bg-black flex items-center justify-center z-50">
      <div class="animate-pulse text-white text-2xl font-light tracking-widest">LOADING...</div>
    </div>

    <!-- Main content -->
    <div v-else class="flex flex-col min-h-screen">
      <MainNavigation />

      <main class="flex-grow">
        <RouterView v-slot="{ Component }">
          <transition name="fade" mode="out-in">
            <component :is="Component" />
          </transition>
        </RouterView>
      </main>

      <MainFooter />
    </div>
  </div>
</template>

<style>
:root {
  --accent-color: #00e0ff;
  --accent-glow: rgba(0, 224, 255, 0.3);
  --bg-color: #000000;
  --text-color: #ffffff;
  --secondary-color: #333333;
}

body {
  font-family: 'Inter', sans-serif;
  background-color: var(--bg-color);
  color: var(--text-color);
  line-height: 1.6;
  overflow-x: hidden;
}

.accent-text {
  color: var(--accent-color);
  text-shadow: 0 0 10px var(--accent-glow);
}

.accent-border {
  border-color: var(--accent-color);
  box-shadow: 0 0 15px var(--accent-glow);
}

@keyframes float {
  0% {
    transform: translateY(0px);
  }

  50% {
    transform: translateY(-10px);
  }

  100% {
    transform: translateY(0px);
  }
}

@keyframes pulse {
  0% {
    box-shadow: 0 0 0 0 var(--accent-glow);
  }

  70% {
    box-shadow: 0 0 0 10px rgba(0, 224, 255, 0);
  }

  100% {
    box-shadow: 0 0 0 0 rgba(0, 224, 255, 0);
  }
}

.glow-effect {
  box-shadow: 0 0 15px var(--accent-glow);
  transition: all 0.3s ease;
}

.glow-effect:hover {
  box-shadow: 0 0 25px var(--accent-glow);
}

.float-animation {
  animation: float 6s ease-in-out infinite;
}

.pulse-animation {
  animation: pulse 2s infinite;
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.3s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}

.container {
  width: 100%;
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 1.5rem;
}

.section {
  padding: 6rem 0;
}

.section-title {
  font-size: 2.5rem;
  font-weight: 700;
  margin-bottom: 2rem;
  position: relative;
  display: inline-block;
  color: white;
  text-shadow: 0 0 15px rgba(255, 255, 255, 0.2);
}

.section-title::after {
  content: '';
  position: absolute;
  bottom: -10px;
  left: 0;
  width: 60px;
  height: 4px;
  background-color: var(--accent-color);
  box-shadow: 0 0 15px var(--accent-glow);
  animation: pulse 2s infinite;
}

.btn {
  display: inline-block;
  padding: 0.75rem 1.5rem;
  background-color: transparent;
  border: 2px solid var(--accent-color);
  color: var(--accent-color);
  font-weight: 500;
  text-transform: uppercase;
  letter-spacing: 1px;
  transition: all 0.3s ease;
  cursor: pointer;
  position: relative;
  overflow: hidden;
  z-index: 1;
  box-shadow: 0 0 10px var(--accent-glow);
}

.btn::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  width: 0%;
  height: 100%;
  background-color: var(--accent-color);
  transition: all 0.3s ease;
  z-index: -1;
}

.btn:hover {
  color: var(--bg-color);
  box-shadow: 0 0 20px var(--accent-glow);
  transform: translateY(-3px);
}

.btn:hover::before {
  width: 100%;
}
</style>
