<script setup lang="ts">
import gsap from 'gsap'
import { onMounted, ref } from 'vue'

interface Skill {
  name: string
  description: string
  category: string
  icon: string
  tools: string[]
}

const frontendSkills: Skill[] = [
  {
    name: 'Vue.js',
    description:
      'Expert in Vue.js ecosystem with extensive experience building complex, scalable applications.',
    category: 'frontend',
    icon: '/vue.png',
    tools: ['Vue 3', 'Vuex', 'Vue Router', 'Composition API', 'Options API'],
  },
  {
    name: 'Nuxt.js',
    description:
      'Proficient in building server-side rendered and static Vue applications with Nuxt.js.',
    category: 'frontend',
    icon: '/nuxt.png',
    tools: ['Nuxt 3', 'SSR', 'Static Site Generation', 'Middleware', 'Modules'],
  },
  {
    name: 'React Native',
    description: 'Skilled in developing cross-platform mobile applications with React Native.',
    category: 'frontend',
    icon: '/react.png',
    tools: ['Expo', 'Navigation', 'Redux', 'Native Modules', 'Animations'],
  },
  {
    name: 'React',
    description: 'Skilled in developing web applications with React.',
    category: 'frontend',
    icon: '/react.png',
    tools: ['Reactjs', 'Tailwind CSS', 'Redux', 'Tanstack Query'],
  },
]

const backendSkills: Skill[] = [
  {
    name: 'Node.js',
    description: 'Extensive experience building scalable server-side applications with Node.js.',
    category: 'backend',
    icon: '/node.png',
    tools: [
      'Express.js',
      'RESTful APIs',
      'Authentication',
      'Middleware',
      'Performance Optimization',
    ],
  },
  {
    name: 'Express',
    description: 'Proficient in creating robust APIs and web applications with Express framework.',
    category: 'backend',
    icon: '/express.png',
    tools: ['Routing', 'Middleware', 'Error Handling', 'Authentication', 'API Design'],
  },
  {
    name: 'Databases',
    description: 'Experience with various database systems, both SQL and NoSQL.',
    category: 'backend',
    icon: '/postgres.png',
    tools: ['MongoDB', 'PostgreSQL', 'MySQL', 'Redis', 'ORM/ODM'],
  },
]

const devopsSkills: Skill[] = [
  {
    name: 'Docker',
    description: 'Proficient in containerization and orchestration with Docker.',
    category: 'devops',
    icon: '🐳',
    tools: [
      'Containerization',
      'Docker Compose',
      'Multi-stage Builds',
      'Optimization',
      'CI/CD Integration',
    ],
  },
  {
    name: 'CI/CD',
    description:
      'Experience setting up and maintaining continuous integration and deployment pipelines.',
    category: 'devops',
    icon: '🔄',
    tools: [
      'GitHub Actions',
      'Jenkins',
      'Automated Testing',
      'Deployment Strategies',
      'Monitoring',
    ],
  },
  {
    name: 'Cloud Services',
    description:
      'Knowledge of cloud platforms and services for deploying and scaling applications.',
    category: 'devops',
    icon: '☁️',
    tools: ['AWS', 'Vercel', 'Netlify', 'Heroku', 'Digital Ocean'],
  },
]

const activeCategory = ref('frontend')

const setActiveCategory = (category: string) => {
  activeCategory.value = category
}

onMounted(() => {
  // Animate elements
  const tl = gsap.timeline()

  tl.from('.skills-title', {
    opacity: 0,
    y: 30,
    duration: 0.8,
  })

  tl.from(
    '.skills-line',
    {
      scaleX: 0,
      duration: 0.8,
      transformOrigin: 'left',
      ease: 'power3.inOut',
    },
    '-=0.6'
  )

  tl.from(
    '.skills-tabs',
    {
      opacity: 0,
      y: 20,
      duration: 0.6,
    },
    '-=0.4'
  )

  // Animate skill cards
  gsap.from('.skill-card', {
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
    <main id="main-content">
      <section class="section bg-black pt-32" role="main" aria-label="Skills and expertise section">
        <div class="container mx-auto px-6">
          <h1 class="skills-title section-title text-white">Expertise</h1>
          <div class="skills-line w-24 h-1 bg-[#00E0FF] mb-12"></div>

          <p class="text-white/70 max-w-3xl mx-auto mb-12">
            With a focus on modern web and mobile development, I bring a comprehensive skill set
            across the entire development stack. My expertise spans frontend, backend, and DevOps
            technologies, allowing me to deliver complete, production-ready solutions.
          </p>

          <!-- Skills tabs -->
          <div class="skills-tabs flex justify-center mb-16">
            <div class="inline-flex border border-gray-800 rounded-md" role="group">
              <button
                @click="setActiveCategory('frontend')"
                :class="[
                  'px-5 py-2 text-sm font-medium tracking-wider uppercase',
                  activeCategory === 'frontend'
                    ? 'bg-[#00E0FF]/10 text-[#00E0FF] border-r border-gray-800'
                    : 'text-white hover:text-[#00E0FF] border-r border-gray-800',
                ]"
              >
                Frontend
              </button>
              <button
                @click="setActiveCategory('backend')"
                :class="[
                  'px-5 py-2 text-sm font-medium tracking-wider uppercase',
                  activeCategory === 'backend'
                    ? 'bg-[#00E0FF]/10 text-[#00E0FF] border-r border-gray-800'
                    : 'text-white hover:text-[#00E0FF] border-r border-gray-800',
                ]"
              >
                Backend
              </button>
              <button
                @click="setActiveCategory('devops')"
                :class="[
                  'px-5 py-2 text-sm font-medium tracking-wider uppercase',
                  activeCategory === 'devops'
                    ? 'bg-[#00E0FF]/10 text-[#00E0FF]'
                    : 'text-white hover:text-[#00E0FF]',
                ]"
              >
                DevOps
              </button>
            </div>
          </div>

          <!-- Frontend skills -->
          <div v-if="activeCategory === 'frontend'" class="grid grid-cols-1 md:grid-cols-2 gap-8">
            <div
              v-for="skill in frontendSkills"
              :key="skill.name"
              class="skill-card bg-gray-900 border border-gray-800 rounded-lg p-6 hover:border-[#00E0FF] transition-colors duration-300"
            >
              <div class="flex items-center mb-4">
                <div
                  class="w-12 h-12 flex items-center justify-center bg-gray-800 rounded-full text-[#00E0FF] mr-4"
                >
                  <img :src="skill.icon" alt="skill icon" class="w-6 h-6" />
                </div>
                <h3 class="text-xl font-bold text-white">{{ skill.name }}</h3>
              </div>
              <p class="text-gray-400 mb-6">{{ skill.description }}</p>
              <div class="flex flex-wrap gap-2">
                <span
                  v-for="tool in skill.tools"
                  :key="tool"
                  class="px-3 py-1 text-xs font-medium bg-gray-800 text-gray-300 rounded-full"
                >
                  {{ tool }}
                </span>
              </div>
            </div>
          </div>

          <!-- Backend skills -->
          <div v-if="activeCategory === 'backend'" class="grid grid-cols-1 md:grid-cols-2 gap-8">
            <div
              v-for="skill in backendSkills"
              :key="skill.name"
              class="skill-card bg-gray-900 border border-gray-800 rounded-lg p-6 hover:border-[#00E0FF] transition-colors duration-300"
            >
              <div class="flex items-center mb-4">
                <div
                  class="w-12 h-12 flex items-center justify-center bg-gray-800 rounded-full text-[#00E0FF] mr-4"
                >
                  <img :src="skill.icon" alt="skill icon" class="w-6 h-6" />
                </div>
                <h3 class="text-xl font-bold text-white">{{ skill.name }}</h3>
              </div>
              <p class="text-gray-400 mb-6">{{ skill.description }}</p>
              <div class="flex flex-wrap gap-2">
                <span
                  v-for="tool in skill.tools"
                  :key="tool"
                  class="px-3 py-1 text-xs font-medium bg-gray-800 text-gray-300 rounded-full"
                >
                  {{ tool }}
                </span>
              </div>
            </div>
          </div>

          <!-- DevOps skills -->
          <div v-if="activeCategory === 'devops'" class="grid grid-cols-1 md:grid-cols-2 gap-8">
            <div
              v-for="skill in devopsSkills"
              :key="skill.name"
              class="skill-card bg-gray-900 border border-gray-800 rounded-lg p-6 hover:border-[#00E0FF] transition-colors duration-300"
            >
              <div class="flex items-center mb-4">
                <div
                  class="w-12 h-12 flex items-center justify-center bg-gray-800 rounded-full text-[#00E0FF] mr-4"
                >
                  <span class="text-2xl">{{ skill.icon }}</span>
                </div>
                <h3 class="text-xl font-bold text-white">{{ skill.name }}</h3>
              </div>
              <p class="text-gray-400 mb-6">{{ skill.description }}</p>
              <div class="flex flex-wrap gap-2">
                <span
                  v-for="tool in skill.tools"
                  :key="tool"
                  class="px-3 py-1 text-xs font-medium bg-gray-800 text-gray-300 rounded-full"
                >
                  {{ tool }}
                </span>
              </div>
            </div>
          </div>
        </div>
      </section>
    </main>
  </div>
</template>
