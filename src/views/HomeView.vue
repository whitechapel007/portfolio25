<script setup lang="ts">
import KineticHero from '../components/KineticHero.vue'
import { ArrowRightIcon } from '@heroicons/vue/24/outline'
import { RouterLink } from 'vue-router'
import Section from '../components/ui/Section.vue'
import Card from '../components/ui/Card.vue'
import Badge from '../components/ui/Badge.vue'

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
</script>

<template>
  <div id="main-content">
    <!-- Kinetic Hero Section -->
    <KineticHero />

    <!-- Selected Projects Section -->
    <Section
      title="Selected Projects"
      subtitle="Here are some of the projects I've worked on recently"
      bg-class="bg-black border-t border-gray-800"
    >
      <div class="flex justify-end mb-8">
        <RouterLink
          to="/projects"
          class="text-[#00E0FF] hover:underline flex items-center transition-colors duration-300"
        >
          View All Projects
          <ArrowRightIcon class="h-5 w-5 ml-1" />
        </RouterLink>
      </div>

      <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
        <!-- Project Cards Loop -->
        <Card
          v-for="project in projects"
          :key="project.id"
          variant="bordered"
          class="group overflow-hidden"
        >
          <template #header>
            <div
              class="relative aspect-video bg-gray-800 flex items-center justify-center overflow-hidden -m-6 -mt-6 mb-0"
            >
              <img
                :src="project.image"
                :alt="project.title"
                class="w-full h-full object-cover transition-transform duration-300 group-hover:scale-110"
              />
              <div
                class="absolute inset-0 bg-[#00E0FF]/10 opacity-0 group-hover:opacity-100 transition-opacity duration-300"
              ></div>
            </div>
          </template>

          <div>
            <h3 class="text-xl font-bold text-white mb-2">{{ project.title }}</h3>
            <p class="text-gray-400 mb-4 line-clamp-2">
              {{ project.description }}
            </p>
            <div class="flex flex-wrap gap-2 mb-4">
              <Badge
                v-for="tech in project.technologies"
                :key="tech"
                variant="secondary"
                class="hover:bg-cyan-500/10 hover:text-cyan-400"
              >
                {{ tech }}
              </Badge>
            </div>
            <a
              :href="project.link"
              target="_blank"
              rel="noopener noreferrer"
              class="text-[#00E0FF] hover:underline inline-flex items-center group transition-colors duration-300"
            >
              View Project
              <ArrowRightIcon
                class="h-4 w-4 ml-1 group-hover:translate-x-1 transition-transform duration-300"
              />
            </a>
          </div>
        </Card>
      </div>
    </Section>
  </div>
</template>
