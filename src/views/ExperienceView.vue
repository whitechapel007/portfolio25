<script setup lang="ts">
import { onMounted } from 'vue'
import gsap from 'gsap'
import { ScrollTrigger } from 'gsap/ScrollTrigger'

gsap.registerPlugin(ScrollTrigger)

interface Experience {
  id: number
  title: string
  company: string
  period: string
  description: string[]
  technologies: string[]
}

interface Education {
  id: number
  degree: string
  institution: string
  period: string
  description: string
}

const experiences: Experience[] = [
  {
    id: 1,
    title: 'Senior Full Stack Developer',
    company: 'Tech Company',
    period: '2020 - Present',
    description: [
      'Led development of modern web applications using Vue.js, Node.js, and Docker.',
      'Implemented CI/CD pipelines and automated testing strategies.',
      'Mentored junior developers and conducted code reviews.',
      'Collaborated with product managers and designers to define product requirements and roadmap.'
    ],
    technologies: ['Vue.js', 'Nuxt.js', 'Node.js', 'Express', 'Docker', 'MongoDB']
  },
  {
    id: 2,
    title: 'Full Stack Developer',
    company: 'Previous Company',
    period: '2018 - 2020',
    description: [
      'Developed and maintained web applications using Vue.js and Express.',
      'Collaborated with design team to implement responsive UI components.',
      'Optimized application performance and implemented security best practices.',
      'Participated in agile development processes and sprint planning.'
    ],
    technologies: ['Vue.js', 'JavaScript', 'Node.js', 'Express', 'PostgreSQL']
  },
  {
    id: 3,
    title: 'Frontend Developer',
    company: 'First Company',
    period: '2016 - 2018',
    description: [
      'Built responsive web interfaces using HTML, CSS, and JavaScript.',
      'Implemented UI components based on design specifications.',
      'Collaborated with backend developers to integrate frontend with APIs.',
      'Participated in user testing and incorporated feedback into development.'
    ],
    technologies: ['HTML', 'CSS', 'JavaScript', 'jQuery', 'Bootstrap']
  }
]

const education: Education[] = [
  {
    id: 1,
    degree: 'Bachelor of Science in Computer Science',
    institution: 'University Name',
    period: '2012 - 2016',
    description: 'Graduated with honors. Focused on software engineering and web development.'
  },
  {
    id: 2,
    degree: 'Full Stack Web Development Bootcamp',
    institution: 'Coding Academy',
    period: '2016',
    description: 'Intensive 12-week program covering modern web development technologies and practices.'
  }
]

onMounted(() => {
  // Animate elements
  gsap.from('.experience-title', {
    opacity: 0,
    y: 30,
    duration: 0.8
  })
  
  // Animate timeline items on scroll
  gsap.utils.toArray('.timeline-item').forEach((item: any, i) => {
    gsap.from(item, {
      opacity: 0,
      y: 50,
      duration: 0.8,
      scrollTrigger: {
        trigger: item,
        start: 'top 80%',
        toggleActions: 'play none none none'
      }
    })
  })
})
</script>

<template>
  <div>
    <section class="bg-white dark:bg-gray-900">
      <div class="section-container">
        <h1 class="experience-title section-title">Experience</h1>
        
        <div class="max-w-4xl mx-auto">
          <!-- Work Experience Timeline -->
          <div class="mb-16">
            <h2 class="text-2xl font-bold text-gray-900 dark:text-white mb-8 text-center">
              Work Experience
            </h2>
            
            <div class="space-y-12">
              <div
                v-for="exp in experiences"
                :key="exp.id"
                class="timeline-item relative pl-10 sm:pl-12"
              >
                <!-- Timeline line -->
                <div class="absolute top-0 left-0 h-full w-0.5 bg-primary-200 dark:bg-primary-900"></div>
                
                <!-- Timeline dot -->
                <div class="absolute top-0 left-0 w-5 h-5 -ml-2.5 rounded-full bg-primary-600"></div>
                
                <div class="bg-white dark:bg-gray-800 rounded-lg shadow-md p-6">
                  <div class="flex flex-col sm:flex-row sm:items-center justify-between mb-4">
                    <div>
                      <h3 class="text-xl font-bold text-gray-900 dark:text-white">{{ exp.title }}</h3>
                      <p class="text-primary-600 font-medium">{{ exp.company }}</p>
                    </div>
                    <div class="mt-2 sm:mt-0">
                      <span class="inline-flex items-center px-3 py-1 rounded-full text-sm font-medium bg-primary-100 text-primary-800 dark:bg-primary-900 dark:text-primary-200">
                        {{ exp.period }}
                      </span>
                    </div>
                  </div>
                  
                  <ul class="mt-4 space-y-2 text-gray-700 dark:text-gray-300">
                    <li v-for="(item, index) in exp.description" :key="index" class="flex items-start">
                      <svg class="h-5 w-5 text-primary-500 mr-2 mt-0.5 flex-shrink-0" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20" fill="currentColor">
                        <path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zm3.707-9.293a1 1 0 00-1.414-1.414L9 10.586 7.707 9.293a1 1 0 00-1.414 1.414l2 2a1 1 0 001.414 0l4-4z" clip-rule="evenodd" />
                      </svg>
                      <span>{{ item }}</span>
                    </li>
                  </ul>
                  
                  <div class="mt-4 flex flex-wrap gap-2">
                    <span
                      v-for="tech in exp.technologies"
                      :key="tech"
                      class="px-2 py-1 text-xs font-medium bg-gray-100 dark:bg-gray-700 rounded-full"
                    >
                      {{ tech }}
                    </span>
                  </div>
                </div>
              </div>
            </div>
          </div>
          
          <!-- Education Timeline -->
          <div>
            <h2 class="text-2xl font-bold text-gray-900 dark:text-white mb-8 text-center">
              Education
            </h2>
            
            <div class="space-y-12">
              <div
                v-for="edu in education"
                :key="edu.id"
                class="timeline-item relative pl-10 sm:pl-12"
              >
                <!-- Timeline line -->
                <div class="absolute top-0 left-0 h-full w-0.5 bg-secondary-200 dark:bg-secondary-900"></div>
                
                <!-- Timeline dot -->
                <div class="absolute top-0 left-0 w-5 h-5 -ml-2.5 rounded-full bg-secondary-600"></div>
                
                <div class="bg-white dark:bg-gray-800 rounded-lg shadow-md p-6">
                  <div class="flex flex-col sm:flex-row sm:items-center justify-between mb-4">
                    <div>
                      <h3 class="text-xl font-bold text-gray-900 dark:text-white">{{ edu.degree }}</h3>
                      <p class="text-secondary-600 font-medium">{{ edu.institution }}</p>
                    </div>
                    <div class="mt-2 sm:mt-0">
                      <span class="inline-flex items-center px-3 py-1 rounded-full text-sm font-medium bg-secondary-100 text-secondary-800 dark:bg-secondary-900 dark:text-secondary-200">
                        {{ edu.period }}
                      </span>
                    </div>
                  </div>
                  
                  <p class="mt-4 text-gray-700 dark:text-gray-300">
                    {{ edu.description }}
                  </p>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>
    
    <!-- Skills & Certifications Preview -->
    <section class="bg-gray-50 dark:bg-gray-800">
      <div class="section-container">
        <h2 class="section-title">Skills & Certifications</h2>
        
        <div class="grid grid-cols-1 md:grid-cols-2 gap-12">
          <!-- Skills -->
          <div>
            <h3 class="text-xl font-bold text-gray-900 dark:text-white mb-6">Key Skills</h3>
            
            <ul class="space-y-4 text-gray-700 dark:text-gray-300">
              <li class="flex items-start">
                <svg class="h-5 w-5 text-primary-500 mr-2 mt-0.5 flex-shrink-0" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20" fill="currentColor">
                  <path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zm3.707-9.293a1 1 0 00-1.414-1.414L9 10.586 7.707 9.293a1 1 0 00-1.414 1.414l2 2a1 1 0 001.414 0l4-4z" clip-rule="evenodd" />
                </svg>
                <span>Full-stack web application development</span>
              </li>
              <li class="flex items-start">
                <svg class="h-5 w-5 text-primary-500 mr-2 mt-0.5 flex-shrink-0" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20" fill="currentColor">
                  <path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zm3.707-9.293a1 1 0 00-1.414-1.414L9 10.586 7.707 9.293a1 1 0 00-1.414 1.414l2 2a1 1 0 001.414 0l4-4z" clip-rule="evenodd" />
                </svg>
                <span>Mobile app development with React Native</span>
              </li>
              <li class="flex items-start">
                <svg class="h-5 w-5 text-primary-500 mr-2 mt-0.5 flex-shrink-0" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20" fill="currentColor">
                  <path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zm3.707-9.293a1 1 0 00-1.414-1.414L9 10.586 7.707 9.293a1 1 0 00-1.414 1.414l2 2a1 1 0 001.414 0l4-4z" clip-rule="evenodd" />
                </svg>
                <span>RESTful API design and implementation</span>
              </li>
              <li class="flex items-start">
                <svg class="h-5 w-5 text-primary-500 mr-2 mt-0.5 flex-shrink-0" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20" fill="currentColor">
                  <path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zm3.707-9.293a1 1 0 00-1.414-1.414L9 10.586 7.707 9.293a1 1 0 00-1.414 1.414l2 2a1 1 0 001.414 0l4-4z" clip-rule="evenodd" />
                </svg>
                <span>Containerization with Docker</span>
              </li>
              <li class="flex items-start">
                <svg class="h-5 w-5 text-primary-500 mr-2 mt-0.5 flex-shrink-0" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20" fill="currentColor">
                  <path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zm3.707-9.293a1 1 0 00-1.414-1.414L9 10.586 7.707 9.293a1 1 0 00-1.414 1.414l2 2a1 1 0 001.414 0l4-4z" clip-rule="evenodd" />
                </svg>
                <span>CI/CD implementation and DevOps practices</span>
              </li>
            </ul>
          </div>
          
          <!-- Certifications -->
          <div>
            <h3 class="text-xl font-bold text-gray-900 dark:text-white mb-6">Certifications</h3>
            
            <div class="space-y-6">
              <div class="bg-white dark:bg-gray-900 p-4 rounded-lg shadow-sm">
                <h4 class="font-semibold text-gray-900 dark:text-white">AWS Certified Developer - Associate</h4>
                <p class="text-sm text-gray-500 dark:text-gray-400">Amazon Web Services • 2022</p>
              </div>
              
              <div class="bg-white dark:bg-gray-900 p-4 rounded-lg shadow-sm">
                <h4 class="font-semibold text-gray-900 dark:text-white">Docker Certified Associate</h4>
                <p class="text-sm text-gray-500 dark:text-gray-400">Docker • 2021</p>
              </div>
              
              <div class="bg-white dark:bg-gray-900 p-4 rounded-lg shadow-sm">
                <h4 class="font-semibold text-gray-900 dark:text-white">Vue.js Developer Certification</h4>
                <p class="text-sm text-gray-500 dark:text-gray-400">Vue Mastery • 2020</p>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>
