<script setup lang="ts">
const currentYear = new Date().getFullYear()
import { emailjsConfig } from '../config/emailjs'

const socialLinks = [
  {
    name: 'GitHub',
    url: 'https://github.com/whitechapel007',
    icon: `<svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="currentColor"><path d="M12 0c-6.626 0-12 5.373-12 12 0 5.302 3.438 9.8 8.207 11.387.599.111.793-.261.793-.577v-2.234c-3.338.726-4.033-1.416-4.033-1.416-.546-1.387-1.333-1.756-1.333-1.756-1.089-.745.083-.729.083-.729 1.205.084 1.839 1.237 1.839 1.237 1.07 1.834 2.807 1.304 3.492.997.107-.775.418-1.305.762-1.604-2.665-.305-5.467-1.334-5.467-5.931 0-1.311.469-2.381 1.236-3.221-.124-.303-.535-1.524.117-3.176 0 0 1.008-.322 3.301 1.23.957-.266 1.983-.399 3.003-.404 1.02.005 2.047.138 3.006.404 2.291-1.552 3.297-1.23 3.297-1.23.653 1.653.242 2.874.118 3.176.77.84 1.235 1.911 1.235 3.221 0 4.609-2.807 5.624-5.479 5.921.43.372.823 1.102.823 2.222v3.293c0 .319.192.694.801.576 4.765-1.589 8.199-6.086 8.199-11.386 0-6.627-5.373-12-12-12z"/></svg>`,
  },
  {
    name: 'LinkedIn',
    url: 'https://www.linkedin.com/in/ebuka-tc/',
    icon: `<svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="currentColor"><path d="M19 0h-14c-2.761 0-5 2.239-5 5v14c0 2.761 2.239 5 5 5h14c2.762 0 5-2.239 5-5v-14c0-2.761-2.238-5-5-5zm-11 19h-3v-11h3v11zm-1.5-12.268c-.966 0-1.75-.79-1.75-1.764s.784-1.764 1.75-1.764 1.75.79 1.75 1.764-.783 1.764-1.75 1.764zm13.5 12.268h-3v-5.604c0-3.368-4-3.113-4 0v5.604h-3v-11h3v1.765c1.396-2.586 7-2.777 7 2.476v6.759z"/></svg>`,
  },
]
</script>

<template>
  <footer class="bg-black border-t border-gray-800 py-12">
    <div class="container mx-auto px-6">
      <div class="grid grid-cols-1 md:grid-cols-3 gap-12">
        <!-- Logo and description -->
        <div>
          <div class="text-2xl font-bold tracking-wider mb-4">
            <span class="text-white">EBUKA</span>
            <span class="text-[#00E0FF]">.</span>
          </div>
          <p class="text-gray-400 mb-6">
            Full-stack developer specializing in modern web and mobile applications.
          </p>
          <div class="flex space-x-4">
            <a
              v-for="link in socialLinks"
              :key="link.name"
              :href="link.url"
              target="_blank"
              rel="noopener noreferrer"
              class="text-gray-400 hover:text-[#00E0FF] transition-colors duration-300"
              :aria-label="link.name"
            >
              <span v-html="link.icon"></span>
            </a>
          </div>
        </div>

        <!-- Quick links -->
        <div>
          <h3 class="text-lg font-semibold text-white mb-4 tracking-wider">QUICK LINKS</h3>
          <ul class="space-y-2">
            <li>
              <RouterLink
                to="/"
                class="text-gray-400 hover:text-[#00E0FF] transition-colors duration-300"
              >
                Home
              </RouterLink>
            </li>
            <li>
              <RouterLink
                to="/about"
                class="text-gray-400 hover:text-[#00E0FF] transition-colors duration-300"
              >
                About
              </RouterLink>
            </li>
            <li>
              <RouterLink
                to="/projects"
                class="text-gray-400 hover:text-[#00E0FF] transition-colors duration-300"
              >
                Work
              </RouterLink>
            </li>
            <li>
              <RouterLink
                to="/skills"
                class="text-gray-400 hover:text-[#00E0FF] transition-colors duration-300"
              >
                Skills
              </RouterLink>
            </li>
            <li>
              <RouterLink
                to="/contact"
                class="text-gray-400 hover:text-[#00E0FF] transition-colors duration-300"
              >
                Contact
              </RouterLink>
            </li>
          </ul>
        </div>

        <!-- Contact info -->
        <div>
          <h3 class="text-lg font-semibold text-white mb-4 tracking-wider">CONTACT</h3>
          <ul class="space-y-4">
            <li class="flex items-start">
              <svg
                class="h-6 w-6 text-[#00E0FF] mr-3 flex-shrink-0"
                xmlns="http://www.w3.org/2000/svg"
                fill="none"
                viewBox="0 0 24 24"
                stroke="currentColor"
              >
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  stroke-width="2"
                  d="M3 8l7.89 5.26a2 2 0 002.22 0L21 8M5 19h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z"
                />
              </svg>
              <span class="text-gray-400">{{ emailjsConfig.recipientEmail }}</span>
            </li>
            <li class="flex items-start">
              <svg
                class="h-6 w-6 text-[#00E0FF] mr-3 flex-shrink-0"
                xmlns="http://www.w3.org/2000/svg"
                fill="none"
                viewBox="0 0 24 24"
                stroke="currentColor"
              >
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  stroke-width="2"
                  d="M17.657 16.657L13.414 20.9a1.998 1.998 0 01-2.827 0l-4.244-4.243a8 8 0 1111.314 0z"
                />
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  stroke-width="2"
                  d="M15 11a3 3 0 11-6 0 3 3 0 016 0z"
                />
              </svg>
              <span class="text-gray-400">Lagos, Nigeria</span>
            </li>
          </ul>
        </div>
      </div>

      <div class="mt-12 pt-8 border-t border-gray-800 text-center">
        <p class="text-gray-500">© {{ currentYear }} Ebuka. All rights reserved.</p>
      </div>
    </div>
  </footer>
</template>
