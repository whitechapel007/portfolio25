<!-- eslint-disable vue/multi-word-component-names -->
<template>
  <section
    :class="['section', bgClass, paddingClass, fullWidth ? 'w-full' : 'container mx-auto px-6']"
  >
    <div v-if="title || subtitle" class="text-center mb-16">
      <h2 v-if="title" class="section-title text-white mb-4">{{ title }}</h2>
      <div class="w-24 h-1 bg-cyan-500 mx-auto mb-6"></div>
      <p v-if="subtitle" class="text-white/70 max-w-3xl mx-auto text-lg">{{ subtitle }}</p>
    </div>

    <slot />
  </section>
</template>

<script setup lang="ts">
interface Props {
  title?: string
  subtitle?: string
  bgClass?: string
  paddingClass?: string
  fullWidth?: boolean
}

withDefaults(defineProps<Props>(), {
  bgClass: 'bg-black',
  paddingClass: 'py-20',
  fullWidth: false,
})
</script>

<style scoped>
.section {
  position: relative;
}

.section-title {
  font-size: 1.875rem;
  font-weight: 700;
}

@media (min-width: 768px) {
  .section-title {
    font-size: 2.25rem;
  }
}
</style>
