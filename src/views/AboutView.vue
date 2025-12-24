<script setup lang="ts">
import gsap from 'gsap'
import { onMounted } from 'vue'
import Section from '../components/ui/Section.vue'
import Card from '../components/ui/Card.vue'

interface Experience {
  title: string
  company: string
  period: string
  description: string
}

interface Education {
  degree: string
  institution: string
  period: string
  description: string
}

const experiences: Experience[] = [
  {
    title: 'Senior Frontend Developer',
    company: 'Credpal',
    period: '2024 - Present',
    description:
      'Led development of modern web applications using Vue.js, Nuxt.js, React, Node.js, and Docker. Implemented CI/CD pipelines and.',
  },
  {
    title: 'Frontend Developer',
    company: 'Imalipay',
    period: '2023 - 2024',
    description:
      'Led frontend development for a fintech payment platform using Vue.js and modern JavaScript frameworks. Implemented secure payment interfaces, optimized application performance, and integrated real-time transaction monitoring systems.',
  },
  {
    title: 'Frontend Developer',
    company: 'Rentaa',
    period: '2019 - 2023',
    description:
      'Built and maintained a comprehensive rental marketplace platform using React and Node.js. Developed property listing interfaces, user authentication systems, and implemented responsive design patterns for mobile-first user experience.',
  },
]

const education: Education[] = [
  {
    degree: 'Bachelor of Engineering in Information and Communication Engineering',
    institution: 'Covenant University',
    period: '2014 - 2019',
    description:
      'Graduated with Second Class Upper Division. Specialized in telecommunications systems, software engineering, and digital signal processing. Developed strong foundation in programming, network protocols, and modern web technologies through hands-on projects.',
  },
]

onMounted(() => {
  // Animate elements
  const tl = gsap.timeline()

  tl.from('.about-title', {
    opacity: 0,
    y: 30,
    duration: 0.8,
  })

  tl.from(
    '.about-line',
    {
      scaleX: 0,
      duration: 0.8,
      transformOrigin: 'left',
      ease: 'power3.inOut',
    },
    '-=0.6'
  )

  tl.from(
    '.about-content',
    {
      opacity: 0,
      y: 20,
      duration: 0.8,
      stagger: 0.1,
    },
    '-=0.6'
  )

  // Animate sections
  gsap.from('.about-image', {
    opacity: 0,
    x: -30,
    duration: 0.8,
    scrollTrigger: {
      trigger: '.about-image',
      start: 'top 80%',
    },
  })

  gsap.from('.experience-section', {
    opacity: 0,
    y: 30,
    duration: 0.8,
    scrollTrigger: {
      trigger: '.experience-section',
      start: 'top 80%',
    },
  })

  gsap.from('.timeline-item', {
    opacity: 0,
    x: -20,
    duration: 0.6,
    stagger: 0.2,
    scrollTrigger: {
      trigger: '.timeline',
      start: 'top 80%',
    },
  })
})
</script>

<template>
  <div>
    <!-- About Section -->
    <main id="main-content">
      <Section title="About Me" bg-class="bg-black pt-32">
        <div class="grid grid-cols-1 lg:grid-cols-2 gap-16 items-center">
          <div class="about-content space-y-6">
            <p class="text-lg text-white/80">
              I'm a passionate full-stack developer with a focus on creating exceptional digital
              experiences. With expertise in modern web and mobile technologies, I bring ideas to
              life through clean, efficient, and maintainable code.
            </p>

            <p class="text-lg text-white/80">
              My journey in software development began with a curiosity about how things work and a
              desire to build solutions that make a difference. Today, I specialize in Vue.js,
              Nuxt.js, React Native, Node.js, Express, and Docker, allowing me to deliver complete,
              production-ready applications.
            </p>

            <p class="text-lg text-white/80">
              I'm passionate about creating intuitive user interfaces, optimizing performance, and
              implementing robust architectures. My approach combines technical expertise with a
              deep understanding of user needs to deliver solutions that exceed expectations.
            </p>

            <p class="text-lg text-white/80">
              When I'm not coding, you can find me exploring new technologies, contributing to
              open-source projects, or sharing my knowledge through mentoring and community
              engagement.
            </p>
          </div>

          <Card variant="bordered" class="about-image relative max-w-md mx-auto">
            <div class="relative z-10 rounded-lg p-1">
              <div class="rounded-lg p-4">
                <div
                  class="aspect-square rounded-lg overflow-hidden flex items-center justify-center"
                >
                  <img src="/tc.png" alt="Ebuka" class="w-full h-full object-cover rounded-md" />
                </div>
              </div>
            </div>

            <!-- Decorative elements -->
            <div
              class="absolute top-1/4 -left-12 w-32 h-32 bg-cyan-500/10 rounded-full blur-3xl"
            ></div>
            <div
              class="absolute bottom-1/4 -right-12 w-40 h-40 bg-cyan-500/5 rounded-full blur-3xl"
            ></div>
          </Card>
        </div>
      </Section>

      <!-- Experience & Education Section -->
      <Section
        title="Experience & Education"
        subtitle="My professional journey and educational background"
        bg-class="bg-black border-t border-gray-800"
      >
        <div class="grid grid-cols-1 lg:grid-cols-2 gap-16">
          <!-- Experience -->
          <div>
            <h3 class="text-2xl font-bold text-white mb-8">Professional Experience</h3>

            <div class="timeline space-y-8">
              <div v-for="(exp, index) in experiences" :key="`exp-${index}`" class="timeline-item">
                <div class="flex flex-col sm:flex-row sm:items-center justify-between mb-2">
                  <h4 class="text-xl font-bold text-white">{{ exp.title }}</h4>
                  <span class="text-sm font-medium text-[#00E0FF]">{{ exp.period }}</span>
                </div>
                <p class="text-lg text-[#00E0FF]/80 mb-2">{{ exp.company }}</p>
                <p class="text-gray-400">{{ exp.description }}</p>
              </div>
            </div>
          </div>

          <!-- Education -->
          <div>
            <h3 class="text-2xl font-bold text-white mb-8">Education</h3>

            <div class="timeline space-y-8">
              <div v-for="(edu, index) in education" :key="`edu-${index}`" class="timeline-item">
                <div class="flex flex-col sm:flex-row sm:items-center justify-between mb-2">
                  <h4 class="text-xl font-bold text-white">{{ edu.degree }}</h4>
                  <span class="text-sm font-medium text-[#00E0FF]">{{ edu.period }}</span>
                </div>
                <p class="text-lg text-[#00E0FF]/80 mb-2">{{ edu.institution }}</p>
                <p class="text-gray-400">{{ edu.description }}</p>
              </div>
            </div>
          </div>
        </div>
      </Section>
    </main>
  </div>
</template>
