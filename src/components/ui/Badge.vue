<!-- eslint-disable vue/multi-word-component-names -->
<template>
  <span
    :class="[
      'badge',
      variant === 'primary' && 'badge-primary',
      variant === 'secondary' && 'badge-secondary',
      variant === 'outline' && 'badge-outline',
      size === 'sm' && 'badge-sm',
      'transition-colors duration-200',
    ]"
  >
    <slot />
  </span>
</template>

<script setup lang="ts">
interface Props {
  variant?: 'primary' | 'secondary' | 'outline'
  size?: 'sm' | 'md'
}

withDefaults(defineProps<Props>(), {
  variant: 'secondary',
  size: 'md',
})
</script>

<style scoped>
.badge {
  display: inline-flex;
  align-items: center;
  padding: 0.25rem 0.75rem;
  font-size: 0.75rem;
  font-weight: 500;
  border-radius: 9999px;
  transition: all 0.2s;
}

.badge-primary {
  background-color: rgba(6, 182, 212, 0.1);
  color: rgb(34, 211, 238);
  border: 1px solid rgba(6, 182, 212, 0.2);
}

.badge-secondary {
  background-color: rgb(55, 65, 81);
  color: rgb(209, 213, 219);
  border: 1px solid rgb(75, 85, 99);
}

.badge-outline {
  background-color: transparent;
  color: rgb(6, 182, 212);
  border: 1px solid rgb(6, 182, 212);
}

.badge-outline:hover {
  background-color: rgb(6, 182, 212);
  color: black;
}

.badge-sm {
  padding: 0.125rem 0.5rem;
  font-size: 0.75rem;
}

.badge:hover {
  transform: scale(1.05);
}
</style>
