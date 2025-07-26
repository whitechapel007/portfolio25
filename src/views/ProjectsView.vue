<script setup lang="ts">
import { ArrowRightIcon, MagnifyingGlassIcon } from '@heroicons/vue/24/outline'
import gsap from 'gsap'
import { computed, onMounted, ref } from 'vue'

interface Project {
  id: number
  title: string
  description: string
  image: string
  technologies: string[]
  category: 'web' | 'mobile' | 'devops' | 'backend'
  link: string
  github: string
}

const projects: Project[] = [
  {
    id: 1,
    title: 'E-Commerce Platform',
    description:
      'A modern e-commerce solution built with Vue.js featuring product catalog, shopping cart, user authentication, and secure payment integration. Includes admin dashboard for inventory management and order tracking.',
    image: '/e-comm.png',
    technologies: ['Vue.js', 'Node.js'],
    link: 'https://white-vue-ecomm.netlify.app',
    category: 'web',
    github: '#',
  },
  {
    id: 2,
    title: 'Twitter Clone',
    description:
      "A full-stack social media platform replicating Twitter's core features including user authentication, tweet composition, real-time timeline updates, user profiles, and follow/unfollow functionality using modern web technologies.",
    image: '/tw.png',
    technologies: ['Nuxt.js', 'Prisma', 'Mongodb'],
    link: 'https://twitter-clone-sooty-eta.vercel.app/',
    category: 'web',
    github: '#',
  },
  {
    id: 3,
    title: 'Document Signing App',
    description:
      'A digital document management and e-signature platform built with React. Features PDF viewing, annotation tools, electronic signature capture, document sharing, and secure authentication for streamlined document workflows.',
    image: '/doc_sign.png',
    technologies: ['React.js', 'react-pdf-viewer'],
    link: 'https://doc-sign-blue.vercel.app',
    category: 'web',
    github: '#',
  },
  {
    id: 4,
    title: 'Covenant Connect Website',
    description:
      'A comprehensive digital platform for a Christian organization featuring event management, community forums, resource sharing, and member engagement tools. Built with responsive design and modern UI/UX principles.',
    image: '/cc.png',
    technologies: ['React.js', 'Node.js'],
    link: 'https://covenant-connect.com/',
    category: 'web',
    github: '#',
  },

  {
    id: 5,
    title: 'Beam Markets Website',
    description:
      'A professional financial services platform showcasing investment products, market analysis tools, and client portfolio management. Features real-time market data integration and responsive design for optimal user experience.',
    image: '/beam.png',
    technologies: ['React.js', 'Tailwind CSS'],
    category: 'web',
    link: 'https://beammarkets.com/',
    github: '#',
  },
  {
    id: 6,
    title: 'Credpal Business Website',
    description:
      'A fintech business platform offering credit solutions and financial services for SMEs. Includes loan application workflows, business analytics dashboard, and secure payment processing with modern design aesthetics.',
    image: '/credpal_bs.png',
    technologies: ['Nuxt.js', 'Tailwind CSS'],
    category: 'web',
    link: 'https://credpal.com/business',
    github: '#',
  },
  {
    id: 7,
    title: 'Rapisurv AI',
    description:
      'An innovative real estate consulting platform powered by artificial intelligence. Features property valuation algorithms, market trend analysis, investment recommendations, and automated reporting for real estate professionals.',
    image: '/rapisurv.png',
    technologies: ['React.js'],
    category: 'web',
    link: 'https://rapisurv.ai/',
    github: '#',
  },

  {
    id: 8,
    title: 'Korrency',
    description:
      'A comprehensive currency exchange platform featuring real-time exchange rates, embedded currency converter, multi-currency wallet management, and secure international money transfer capabilities with competitive rates.',
    image: '/korrency.png',
    technologies: ['React.js'],
    category: 'web',
    link: 'https://korrency.com/',
    github: '#',
  },
  {
    id: 9,
    title: 'Imalipay API Documentation',
    description:
      'A comprehensive API documentation platform for a fintech payment gateway. Features interactive API explorer, code examples, authentication guides, and developer resources built with Docusaurus for optimal developer experience.',
    image: '/imali-docs.png',
    technologies: ['React.js', 'Docusaurus'],
    category: 'web',
    link: 'https://docs.imalipay.com/api#/',
    github: '#',
  },
  {
    id: 10,
    title: 'Jump Social',
    description:
      'A dynamic social networking platform enabling content creators to connect, share, and monetize their content. Features user onboarding, content streaming, social interactions, and creator monetization tools with modern UI design.',
    image: '/jump.png',
    technologies: ['React.js'],
    category: 'web',
    link: 'https://frontend.streamjump.info/onboarding',
    github: '#',
  },
  {
    id: 11,
    title: 'Fitness Tracker',
    description:
      'A comprehensive mobile fitness application for tracking workouts, nutrition, and fitness progress. Features exercise logging, meal planning, progress analytics, social challenges, and personalized workout recommendations.',
    image: '💪',
    technologies: ['React Native', 'Node.js', 'Express', 'MongoDB'],
    category: 'mobile',
    link: '#',
    github: '#',
  },
]

const activeFilter = ref('all')
const searchQuery = ref('')

const filteredProjects = computed(() => {
  let filtered = projects

  // Filter by category
  if (activeFilter.value !== 'all') {
    filtered = filtered.filter((project) => project.category === activeFilter.value)
  }

  // Filter by search query
  if (searchQuery.value) {
    const query = searchQuery.value.toLowerCase()
    filtered = filtered.filter(
      (project) =>
        project.title.toLowerCase().includes(query) ||
        project.description.toLowerCase().includes(query) ||
        project.technologies.some((tech) => tech.toLowerCase().includes(query))
    )
  }

  return filtered
})

const setFilter = (filter: string) => {
  activeFilter.value = filter
}

onMounted(() => {
  // Animate elements
  const tl = gsap.timeline()

  tl.from('.projects-title', {
    opacity: 0,
    y: 30,
    duration: 0.8,
  })

  tl.from(
    '.projects-line',
    {
      scaleX: 0,
      duration: 0.8,
      transformOrigin: 'left',
      ease: 'power3.inOut',
    },
    '-=0.6'
  )

  tl.from(
    '.projects-filters',
    {
      opacity: 0,
      y: 20,
      duration: 0.6,
    },
    '-=0.4'
  )

  // Animate project cards with stagger
  gsap.from('.project-card', {
    opacity: 0,
    y: 30,
    duration: 0.8,
    stagger: 0.1,
    delay: 0.6,
  })
})
</script>

<template>
  <div>
    <section class="section bg-black pt-32">
      <div class="container mx-auto px-6">
        <h1 class="projects-title section-title text-white">My Work</h1>
        <div class="projects-line w-24 h-1 bg-[#00E0FF] mb-12"></div>

        <p class="text-white/70 max-w-3xl mx-auto mb-12">
          Here are some of the projects I've worked on. Each project demonstrates different skills
          and technologies.
        </p>

        <!-- Filters -->
        <div class="projects-filters mb-16">
          <div class="flex flex-col sm:flex-row justify-center items-center gap-6">
            <div class="inline-flex border border-gray-800 rounded-md" role="group">
              <button
                @click="setFilter('all')"
                :class="[
                  'px-5 py-2 text-sm font-medium tracking-wider uppercase',
                  activeFilter === 'all'
                    ? 'bg-[#00E0FF]/10 text-[#00E0FF] border-r border-gray-800'
                    : 'text-white hover:text-[#00E0FF] border-r border-gray-800',
                ]"
              >
                All
              </button>
              <button
                @click="setFilter('web')"
                :class="[
                  'px-5 py-2 text-sm font-medium tracking-wider uppercase',
                  activeFilter === 'web'
                    ? 'bg-[#00E0FF]/10 text-[#00E0FF] border-r border-gray-800'
                    : 'text-white hover:text-[#00E0FF] border-r border-gray-800',
                ]"
              >
                Web
              </button>
              <button
                @click="setFilter('mobile')"
                :class="[
                  'px-5 py-2 text-sm font-medium tracking-wider uppercase',
                  activeFilter === 'mobile'
                    ? 'bg-[#00E0FF]/10 text-[#00E0FF]'
                    : 'text-white hover:text-[#00E0FF]',
                ]"
              >
                Mobile
              </button>
            </div>

            <div class="w-full sm:w-auto">
              <div class="relative">
                <input
                  v-model="searchQuery"
                  type="text"
                  placeholder="Search projects..."
                  class="w-full px-4 py-2 pl-10 bg-gray-900 border border-gray-800 rounded-md text-white focus:outline-none focus:border-[#00E0FF] transition-colors"
                />
                <MagnifyingGlassIcon
                  class="h-5 w-5 absolute left-3 top-1/2 transform -translate-y-1/2 text-gray-500"
                />
              </div>
            </div>
          </div>
        </div>

        <!-- Projects grid -->
        <div
          v-if="filteredProjects.length > 0"
          class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8"
        >
          <div
            v-for="project in filteredProjects"
            :key="project.id"
            class="project-card group bg-gray-900 border border-gray-800 rounded-lg overflow-hidden hover:border-[#00E0FF] transition-colors duration-300"
          >
            <div
              class="relative aspect-video bg-gray-800 flex items-center justify-center overflow-hidden"
            >
              <img
                :src="project.image"
                :alt="project.title"
                class="w-full h-full object-cover group-hover:scale-110 transition-transform duration-300"
              />
              <div
                class="absolute inset-0 bg-[#00E0FF]/10 opacity-0 group-hover:opacity-100 transition-opacity duration-300"
              ></div>
            </div>
            <div class="p-6">
              <h3 class="text-xl font-bold text-white mb-2">{{ project.title }}</h3>
              <p class="text-gray-400 mb-4 h-12 line-clamp-2">
                {{ project.description }}
              </p>
              <div class="flex flex-wrap gap-2 mb-4">
                <span
                  v-for="tech in project.technologies"
                  :key="tech"
                  class="px-2 py-1 text-xs font-medium bg-gray-800 text-gray-300 rounded-full"
                >
                  {{ tech }}
                </span>
              </div>
              <div class="flex space-x-4 mt-6">
                <a
                  :href="project.link"
                  target="_blank"
                  rel="noopener noreferrer"
                  class="text-[#00E0FF] hover:underline inline-flex items-center"
                >
                  Live Demo
                  <ArrowRightIcon class="h-4 w-4 ml-1" />
                </a>
              </div>
            </div>
          </div>
        </div>

        <!-- No results message -->
        <div v-else class="text-center py-16">
          <p class="text-white/70 text-lg mb-6">No projects found matching your criteria.</p>
          <button
            @click="
              () => {
                activeFilter = 'all'
                searchQuery = ''
              }
            "
            class="btn"
          >
            Reset Filters
          </button>
        </div>
      </div>
    </section>
  </div>
</template>
