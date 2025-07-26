<script setup lang="ts">
import emailjs from '@emailjs/browser'
import gsap from 'gsap'
import { onMounted, ref } from 'vue'
import { emailjsConfig } from '../config/emailjs'

emailjs.init({
  publicKey: emailjsConfig.publicKey,
  // Do not allow headless browsers
  blockHeadless: false,

  limitRate: {
    // Set the limit rate for the application
    id: 'app',
    // Allow 1 request per 10s
    throttle: 10000,
  },
})

const name = ref('')
const email = ref('')
const subject = ref('')
const message = ref('')
const isSubmitting = ref(false)
const submitSuccess = ref(false)
const submitError = ref(false)

const handleSubmit = async () => {
  isSubmitting.value = true

  try {
    // Send email using EmailJS
    await emailjs.send(emailjsConfig.serviceID, emailjsConfig.templateID, {
      from_name: name.value,
      subject: subject.value,
      message: message.value,
      to_email: email.value,
    })

    // Reset form
    name.value = ''
    email.value = ''
    subject.value = ''
    message.value = ''

    submitSuccess.value = true
    setTimeout(() => {
      submitSuccess.value = false
    }, 5000)
  } catch (error) {
    console.error('EmailJS Error:', error)
    submitError.value = true
    setTimeout(() => {
      submitError.value = false
    }, 5000)
  } finally {
    isSubmitting.value = false
  }
}

onMounted(() => {
  // Animate elements
  const tl = gsap.timeline()

  tl.from('.contact-title', {
    opacity: 0,
    y: 30,
    duration: 0.8,
  })

  tl.from(
    '.contact-line',
    {
      scaleX: 0,
      duration: 0.8,
      transformOrigin: 'left',
      ease: 'power3.inOut',
    },
    '-=0.6'
  )

  tl.from(
    '.contact-description',
    {
      opacity: 0,
      y: 20,
      duration: 0.6,
    },
    '-=0.4'
  )

  tl.from(
    '.contact-form',
    {
      opacity: 0,
      y: 30,
      duration: 0.8,
    },
    '-=0.2'
  )

  tl.from(
    '.contact-info',
    {
      opacity: 0,
      y: 30,
      duration: 0.8,
    },
    '-=0.6'
  )
})
</script>

<template>
  <div>
    <section class="section bg-black pt-32">
      <div class="container mx-auto px-6">
        <h1 class="contact-title section-title text-white">Contact Me</h1>
        <div class="contact-line w-24 h-1 bg-[#00E0FF] mb-12"></div>

        <p class="contact-description text-white/70 max-w-3xl mx-auto mb-16">
          Have a question or want to work together? Feel free to reach out to me using the form
          below.
        </p>

        <div class="grid grid-cols-1 lg:grid-cols-2 gap-16">
          <!-- Contact Form -->
          <div class="contact-form bg-gray-900 border border-gray-800 rounded-lg p-6 md:p-8">
            <h2 class="text-2xl font-bold text-white mb-8">Send a Message</h2>

            <form @submit.prevent="handleSubmit" class="space-y-6">
              <div>
                <label for="name" class="block text-sm font-medium text-gray-300 mb-2">
                  Name
                </label>
                <input
                  id="name"
                  v-model="name"
                  type="text"
                  required
                  class="w-full px-4 py-3 bg-gray-800 border border-gray-700 rounded-md text-white focus:outline-none focus:border-[#00E0FF] transition-colors"
                />
              </div>

              <div>
                <label for="email" class="block text-sm font-medium text-gray-300 mb-2">
                  Email
                </label>
                <input
                  id="email"
                  v-model="email"
                  type="email"
                  required
                  class="w-full px-4 py-3 bg-gray-800 border border-gray-700 rounded-md text-white focus:outline-none focus:border-[#00E0FF] transition-colors"
                />
              </div>

              <div>
                <label for="subject" class="block text-sm font-medium text-gray-300 mb-2">
                  Subject
                </label>
                <input
                  id="subject"
                  v-model="subject"
                  type="text"
                  required
                  class="w-full px-4 py-3 bg-gray-800 border border-gray-700 rounded-md text-white focus:outline-none focus:border-[#00E0FF] transition-colors"
                />
              </div>

              <div>
                <label for="message" class="block text-sm font-medium text-gray-300 mb-2">
                  Message
                </label>
                <textarea
                  id="message"
                  v-model="message"
                  rows="5"
                  required
                  class="w-full px-4 py-3 bg-gray-800 border border-gray-700 rounded-md text-white focus:outline-none focus:border-[#00E0FF] transition-colors"
                ></textarea>
              </div>

              <div class="pt-4">
                <button
                  type="submit"
                  class="w-full btn flex items-center justify-center"
                  :disabled="isSubmitting"
                >
                  <ArrowPathIcon
                    v-if="isSubmitting"
                    class="animate-spin -ml-1 mr-2 h-4 w-4 text-white"
                  />
                  {{ isSubmitting ? 'Sending...' : 'Send Message' }}
                </button>
              </div>

              <!-- Success message -->
              <div
                v-if="submitSuccess"
                class="bg-[#00E0FF]/10 border border-[#00E0FF] text-[#00E0FF] px-4 py-3 rounded-md"
                role="alert"
              >
                <strong class="font-bold">Success!</strong>
                <span class="block sm:inline"> Your message has been sent successfully.</span>
              </div>

              <!-- Error message -->
              <div
                v-if="submitError"
                class="bg-red-900/20 border border-red-500 text-red-500 px-4 py-3 rounded-md"
                role="alert"
              >
                <strong class="font-bold">Error!</strong>
                <span class="block sm:inline">
                  There was an error sending your message. Please try again.</span
                >
              </div>
            </form>
          </div>

          <!-- Contact Information -->
          <div class="contact-info space-y-12">
            <div>
              <h2 class="text-2xl font-bold text-white mb-6">Contact Information</h2>

              <div class="space-y-6">
                <div class="flex items-start">
                  <div class="flex-shrink-0">
                    <EnvelopeIcon class="h-6 w-6 text-[#00E0FF]" />
                  </div>
                  <div class="ml-4">
                    <p class="text-base font-medium text-white">Email</p>
                    <p class="text-gray-400">ebukareed@gmail.com</p>
                  </div>
                </div>

                <div class="flex items-start">
                  <div class="flex-shrink-0">
                    <MapPinIcon class="h-6 w-6 text-[#00E0FF]" />
                  </div>
                  <div class="ml-4">
                    <p class="text-base font-medium text-white">Location</p>
                    <p class="text-gray-400">Lagos</p>
                  </div>
                </div>
              </div>
            </div>

            <!-- Social Links -->
            <div>
              <h2 class="text-2xl font-bold text-white mb-6">Connect With Me</h2>

              <div class="flex space-x-6">
                <a
                  href="https://github.com/whitechapel007"
                  target="_blank"
                  rel="noopener noreferrer"
                  class="text-gray-400 hover:text-[#00E0FF] transition-colors duration-300"
                >
                  <span class="sr-only">GitHub</span>
                  <svg class="h-6 w-6" fill="currentColor" viewBox="0 0 24 24" aria-hidden="true">
                    <path
                      d="M12 0c-6.626 0-12 5.373-12 12 0 5.302 3.438 9.8 8.207 11.387.599.111.793-.261.793-.577v-2.234c-3.338.726-4.033-1.416-4.033-1.416-.546-1.387-1.333-1.756-1.333-1.756-1.089-.745.083-.729.083-.729 1.205.084 1.839 1.237 1.839 1.237 1.07 1.834 2.807 1.304 3.492.997.107-.775.418-1.305.762-1.604-2.665-.305-5.467-1.334-5.467-5.931 0-1.311.469-2.381 1.236-3.221-.124-.303-.535-1.524.117-3.176 0 0 1.008-.322 3.301 1.23.957-.266 1.983-.399 3.003-.404 1.02.005 2.047.138 3.006.404 2.291-1.552 3.297-1.23 3.297-1.23.653 1.653.242 2.874.118 3.176.77.84 1.235 1.911 1.235 3.221 0 4.609-2.807 5.624-5.479 5.921.43.372.823 1.102.823 2.222v3.293c0 .319.192.694.801.576 4.765-1.589 8.199-6.086 8.199-11.386 0-6.627-5.373-12-12-12z"
                    />
                  </svg>
                </a>

                <a
                  href="https://www.linkedin.com/in/ebuka-tc/"
                  target="_blank"
                  rel="noopener noreferrer"
                  class="text-gray-400 hover:text-[#00E0FF] transition-colors duration-300"
                >
                  <span class="sr-only">LinkedIn</span>
                  <svg class="h-6 w-6" fill="currentColor" viewBox="0 0 24 24" aria-hidden="true">
                    <path
                      d="M20.447 20.452h-3.554v-5.569c0-1.328-.027-3.037-1.852-3.037-1.853 0-2.136 1.445-2.136 2.939v5.667H9.351V9h3.414v1.561h.046c.477-.9 1.637-1.85 3.37-1.85 3.601 0 4.267 2.37 4.267 5.455v6.286zM5.337 7.433c-1.144 0-2.063-.926-2.063-2.065 0-1.138.92-2.063 2.063-2.063 1.14 0 2.064.925 2.064 2.063 0 1.139-.925 2.065-2.064 2.065zm1.782 13.019H3.555V9h3.564v11.452zM22.225 0H1.771C.792 0 0 .774 0 1.729v20.542C0 23.227.792 24 1.771 24h20.451C23.2 24 24 23.227 24 22.271V1.729C24 .774 23.2 0 22.222 0h.003z"
                    />
                  </svg>
                </a>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>
