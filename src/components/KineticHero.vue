<script setup lang="ts">
import { onMounted, ref } from 'vue'
import gsap from 'gsap'
import { ScrollTrigger } from 'gsap/ScrollTrigger'

gsap.registerPlugin(ScrollTrigger)

const heroRef = ref<HTMLElement>()
const titleRef = ref<HTMLElement>()
const subtitleRef = ref<HTMLElement>()

onMounted(() => {
  if (!heroRef.value || !titleRef.value || !subtitleRef.value) return

  const tl = gsap.timeline()

  // Split title into characters for individual animation
  const titleChars = gsap.utils.toArray('.title-char', titleRef.value)

  // Initial origami fold setup
  gsap.set(titleChars, {
    rotationY: -90,
    transformOrigin: 'center center',
    backfaceVisibility: 'hidden',
  })

  gsap.set('.shadow-layer', {
    opacity: 0,
    scale: 0.8,
  })

  // Origami unfold animation
  tl.to(titleChars, {
    rotationY: 0,
    duration: 1.2,
    ease: 'back.out(1.7)',
    stagger: 0.1,
  })

  // Shadow layers appear
  tl.to(
    '.shadow-layer',
    {
      opacity: 0.3,
      scale: 1,
      duration: 0.8,
      stagger: 0.2,
    },
    '-=0.5'
  )

  // Subtitle typewriter effect
  const subtitleText = subtitleRef.value.textContent || ''
  gsap.set(subtitleRef.value, { textContent: '' })

  const chars = subtitleText.split('')
  chars.forEach((char, index) => {
    tl.to(
      {},
      {
        duration: 0.05,
        onComplete: () => {
          if (subtitleRef.value) {
            subtitleRef.value.textContent += char
          }
        },
      },
      `+=${index * 0.03}`
    )
  })

  // Scroll-triggered velocity distortion
  ScrollTrigger.create({
    trigger: heroRef.value,
    start: 'top center',
    end: 'bottom center',
    scrub: true,
    onUpdate: (self) => {
      const velocity = self.getVelocity()
      const distortion = Math.min(Math.abs(velocity) * 0.001, 20)

      gsap.set(titleChars, {
        rotationX: distortion * 0.5,
        rotationY: distortion * 0.3,
        scale: 1 + distortion * 0.01,
      })

      gsap.set('.shadow-layer', {
        x: distortion * 0.2,
        y: distortion * 0.1,
      })
    },
  })

  // Magnetic mouse effect
  const handleMouseMove = (e: MouseEvent) => {
    const rect = heroRef.value!.getBoundingClientRect()
    const x = e.clientX - rect.left
    const y = e.clientY - rect.top

    gsap.to('.shadow-layer', {
      x: (x - rect.width / 2) * 0.05,
      y: (y - rect.height / 2) * 0.05,
      duration: 0.5,
      ease: 'power2.out',
    })
  }

  heroRef.value.addEventListener('mousemove', handleMouseMove)
})
</script>

<template>
  <section
    ref="heroRef"
    class="relative min-h-screen flex items-center justify-center bg-black overflow-hidden"
    role="banner"
    aria-label="Kinetic hero section"
  >
    <!-- Background origami shapes -->
    <div class="absolute inset-0 opacity-10">
      <div
        class="shadow-layer absolute top-1/4 left-1/4 w-64 h-64 bg-cyan-500/20 transform rotate-45"
      ></div>
      <div
        class="shadow-layer absolute bottom-1/4 right-1/4 w-48 h-48 bg-cyan-400/15 transform -rotate-12"
      ></div>
      <div
        class="shadow-layer absolute top-1/2 left-1/2 w-32 h-32 bg-cyan-600/25 transform rotate-67 -translate-x-1/2 -translate-y-1/2"
      ></div>
    </div>

    <div class="container mx-auto px-6 text-center relative z-10">
      <!-- Main title with origami effect -->
      <h1
        ref="titleRef"
        class="text-7xl md:text-9xl font-black text-white mb-8 leading-none"
        style="font-family: 'Inter', sans-serif; font-weight: 900"
      >
        <span class="title-char inline-block">I</span>
        <span class="title-char inline-block">'</span>
        <span class="title-char inline-block">m</span>
        <span class="title-char inline-block">&nbsp;</span>
        <span class="title-char inline-block">E</span>
        <span class="title-char inline-block">b</span>
        <span class="title-char inline-block">u</span>
        <span class="title-char inline-block">k</span>
        <span class="title-char inline-block">a</span>
      </h1>

      <!-- Subtitle with typewriter effect -->
      <div
        ref="subtitleRef"
        class="text-2xl md:text-4xl font-light text-cyan-400 mb-12 h-16 flex items-center justify-center"
        style="font-family: 'Inter', sans-serif"
      >
        Full Stack Developer
      </div>

      <!-- Call to action -->
      <div class="flex flex-col sm:flex-row gap-6 justify-center">
        <router-link
          to="/projects"
          class="px-8 py-4 bg-cyan-500 text-black font-bold text-lg uppercase tracking-wider hover:bg-cyan-400 transition-colors duration-300 transform hover:scale-105"
        >
          View My Work
        </router-link>
        <router-link
          to="/contact"
          class="px-8 py-4 border-2 border-cyan-500 text-cyan-500 font-bold text-lg uppercase tracking-wider hover:bg-cyan-500 hover:text-black transition-all duration-300"
        >
          Get In Touch
        </router-link>
      </div>
    </div>

    <!-- Scroll indicator -->
    <div class="absolute bottom-8 left-1/2 transform -translate-x-1/2">
      <div class="w-6 h-10 border-2 border-cyan-500 rounded-full flex justify-center">
        <div class="w-1 h-3 bg-cyan-500 rounded-full mt-2 animate-bounce"></div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.title-char {
  display: inline-block;
  transform-style: preserve-3d;
}

/* Ensure smooth animations */
.shadow-layer {
  will-change: transform, opacity;
}
</style>
