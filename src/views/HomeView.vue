<script setup lang="ts">
import { ArrowRightIcon, ChevronDownIcon } from '@heroicons/vue/24/outline'
import gsap from 'gsap'
import { onMounted, ref } from 'vue'
import { RouterLink } from 'vue-router'

const roles = [
  'Full Stack Developer',
  'Vue.js Expert',
  'Nuxt.js Developer',
  'React Native Developer',
  'Node.js Engineer',
  'Docker Specialist',
]

const projects = [
  {
    id: 1,
    title: 'E-Commerce Platform',
    description:
      'A modern e-commerce solution featuring product catalog, shopping cart, and secure payment integration with admin dashboard.',
    image: '/e-comm.png',
    technologies: ['Vue.js', 'Node.js'],
    link: 'https://white-vue-ecomm.netlify.app',
  },
  {
    id: 2,
    title: 'Twitter Clone',
    description:
      'A full-stack social media platform with user authentication, tweet composition, and real-time timeline updates.',
    image: '/tw.png',
    technologies: ['Nuxt.js', 'Prisma', 'Mongodb'],
    link: 'https://twitter-clone-sooty-eta.vercel.app/',
  },
  {
    id: 3,
    title: 'Document Signing App',
    description:
      'A digital document management platform with PDF viewing, annotation tools, and electronic signature capabilities.',
    image: '/doc_sign.png',
    technologies: ['React.js', 'react-pdf-viewer'],
    link: 'https://doc-sign-blue.vercel.app',
  },
]

const currentRoleIndex = ref(0)
const typedText = ref('')
const isDeleting = ref(false)
const typingSpeed = ref(100)

const typeEffect = () => {
  const currentRole = roles[currentRoleIndex.value]

  if (!isDeleting.value) {
    typedText.value = currentRole.substring(0, typedText.value.length + 1)

    if (typedText.value === currentRole) {
      isDeleting.value = true
      typingSpeed.value = 1500 // Pause at the end
    }
  } else {
    typedText.value = currentRole.substring(0, typedText.value.length - 1)

    if (typedText.value === '') {
      isDeleting.value = false
      currentRoleIndex.value = (currentRoleIndex.value + 1) % roles.length
      typingSpeed.value = 500 // Pause before typing next word
    }
  }

  setTimeout(typeEffect, isDeleting.value ? 50 : typingSpeed.value)
}

onMounted(() => {
  setTimeout(typeEffect, 1000)

  // Animate elements
  const tl = gsap.timeline()

  tl.from('.hero-content', {
    opacity: 0,
    y: 50,
    duration: 1,
    ease: 'power3.out',
  })

  tl.from(
    '.hero-image',
    {
      opacity: 0,
      x: 50,
      duration: 1,
      ease: 'power3.out',
    },
    '-=0.5'
  )

  tl.from('.scroll-indicator', {
    opacity: 0,
    y: -20,
    duration: 0.6,
    repeat: -1,
    yoyo: true,
    ease: 'power1.inOut',
  })
})
</script>

<template>
  <div>
    <!-- Hero Section -->
    <main id="main-content">
      <section
        class="min-h-screen flex items-center bg-black relative overflow-hidden"
        role="banner"
        aria-label="Hero section"
      >
        <!-- Background elements -->
        <div class="absolute inset-0 z-0">
          <div
            class="absolute top-1/4 left-1/4 w-96 h-96 bg-[#00E0FF]/5 rounded-full blur-3xl"
          ></div>
          <div
            class="absolute bottom-1/4 right-1/4 w-96 h-96 bg-[#00E0FF]/5 rounded-full blur-3xl"
          ></div>
        </div>

        <div class="container mx-auto px-6 py-12 relative z-10">
          <div class="grid grid-cols-1 lg:grid-cols-2 gap-16 items-center">
            <div class="hero-content">
              <h1 class="text-5xl md:text-7xl font-bold text-white mb-6">
                I'm <span class="accent-text">Ebuka</span>
              </h1>

              <div class="text-2xl md:text-3xl font-light text-white/80 mb-8 h-10">
                <span class="accent-text">{{ typedText }}</span
                ><span class="animate-pulse">|</span>
              </div>

              <p class="text-lg text-white/70 mb-10 max-w-xl">
                I create exceptional digital experiences through clean, efficient code. Specializing
                in modern web and mobile development with Vue, Nuxt, React Native, Node, Express,
                and Docker.
              </p>

              <div class="flex flex-wrap gap-6 mb-12">
                <RouterLink to="/projects" class="btn"> View My Work </RouterLink>
                <RouterLink
                  to="/contact"
                  class="text-white hover:text-[#00E0FF] transition-colors duration-300 flex items-center"
                >
                  Contact Me
                  <ArrowRightIcon class="h-5 w-5 ml-2" />
                </RouterLink>
              </div>

              <div class="scroll-indicator hidden md:flex items-center text-white/30 text-sm">
                <ChevronDownIcon class="w-5 h-5 mr-3" />
                SCROLL DOWN
              </div>
            </div>

            <div class="hero-image relative hidden lg:block">
              <div class="relative z-10 float-animation">
                <div
                  class="aspect-square w-full max-w-md mx-auto bg-gray-900 border-2 border-[#00E0FF] rounded-lg p-1 glow-effect"
                >
                  <div
                    class="w-full h-full bg-gray-800 rounded-md flex items-center justify-center"
                  >
                    <img src="/tc.png" alt="Ebuka" class="w-full h-full object-cover rounded-md" />
                  </div>
                </div>
              </div>

              <!-- Decorative elements -->
              <div
                class="absolute top-1/4 -right-8 w-24 h-24 bg-[#00E0FF]/20 rounded-full blur-xl pulse-animation"
              ></div>
              <div
                class="absolute bottom-1/4 -left-8 w-32 h-32 bg-[#00E0FF]/10 rounded-full blur-xl pulse-animation"
                style="animation-delay: 1s"
              ></div>
              <div
                class="absolute top-1/2 left-1/2 -translate-x-1/2 -translate-y-1/2 w-full h-full bg-[#00E0FF]/5 rounded-full blur-3xl pulse-animation"
                style="animation-delay: 0.5s"
              ></div>
            </div>
          </div>
        </div>
      </section>

      <!-- Selected Projects Section -->
      <section class="section bg-black border-t border-gray-800 projects-section">
        <div class="container mx-auto px-6 py-20">
          <div class="flex flex-col md:flex-row md:items-end justify-between mb-16">
            <div>
              <h2 class="text-3xl md:text-4xl font-bold text-white">Selected Projects</h2>
              <div class="w-24 h-1 bg-[#00E0FF] mt-4"></div>
            </div>
            <RouterLink
              to="/projects"
              class="text-[#00E0FF] mt-4 md:mt-0 hover:underline flex items-center"
            >
              View All Projects
              <ArrowRightIcon class="h-5 w-5 ml-1" />
            </RouterLink>
          </div>

          <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
            <!-- Project Cards Loop -->
            <div
              v-for="project in projects"
              :key="project.id"
              class="project-card group bg-gray-900 border border-gray-800 rounded-lg overflow-hidden hover:border-[#00E0FF] transition-all duration-300 hover:-translate-y-2 glow-effect"
            >
              <div
                class="relative aspect-video bg-gray-800 flex items-center justify-center overflow-hidden"
              >
                <img :src="project.image" :alt="project.title" />
                <div
                  class="absolute inset-0 bg-[#00E0FF]/10 opacity-0 group-hover:opacity-100 transition-opacity duration-300"
                ></div>
              </div>
              <div class="p-6">
                <h3 class="text-xl font-bold text-white mb-2">{{ project.title }}</h3>
                <p class="text-gray-400 mb-4 line-clamp-2">
                  {{ project.description }}
                </p>
                <div class="flex flex-wrap gap-2 mb-4">
                  <span
                    v-for="tech in project.technologies"
                    :key="tech"
                    class="px-2 py-1 text-xs font-medium bg-gray-800 text-gray-300 rounded-full hover:bg-[#00E0FF]/20 transition-colors duration-300"
                  >
                    {{ tech }}
                  </span>
                </div>
                <a
                  :href="project.link"
                  class="text-[#00E0FF] hover:underline inline-flex items-center group"
                >
                  View Project
                  <ArrowRightIcon
                    class="h-4 w-4 ml-1 group-hover:translate-x-1 transition-transform duration-300"
                  />
                </a>
              </div>
            </div>
          </div>
        </div>
      </section>
    </main>
  </div>
</template>
