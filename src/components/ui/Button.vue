<!-- eslint-disable vue/multi-word-component-names -->
<template>
  <button
    :class="[
      'btn',
      variant === 'primary' && 'btn-primary',
      variant === 'secondary' && 'btn-secondary',
      variant === 'outline' && 'btn-outline',
      size === 'sm' && 'btn-sm',
      size === 'lg' && 'btn-lg',
      disabled && 'btn-disabled',
      loading && 'btn-loading',
      fullWidth && 'w-full',
      'transition-all duration-300',
    ]"
    :disabled="disabled || loading"
    @click="$emit('click', $event)"
  >
    <ArrowPathIcon v-if="loading" class="animate-spin -ml-1 mr-2 h-4 w-4" aria-hidden="true" />
    <slot />
  </button>
</template>

<script setup lang="ts">
import { ArrowPathIcon } from '@heroicons/vue/24/outline'

interface Props {
  variant?: 'primary' | 'secondary' | 'outline'
  size?: 'sm' | 'lg'
  disabled?: boolean
  loading?: boolean
  fullWidth?: boolean
}

withDefaults(defineProps<Props>(), {
  variant: 'primary',
  size: 'lg',
})

defineEmits<{
  click: [event: Event]
}>()
</script>

<style scoped>
.btn {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  padding: 0.75rem 1.5rem;
  font-weight: 700;
  font-size: 0.875rem;
  text-transform: uppercase;
  letter-spacing: 0.05em;
  border-radius: 0.375rem;
  border-width: 2px;
  transition: all 0.3s;
}

.btn-primary {
  background-color: rgb(6, 182, 212);
  color: black;
  border-color: rgb(6, 182, 212);
}

.btn-primary:hover {
  background-color: rgb(34, 211, 238);
  border-color: rgb(34, 211, 238);
  transform: scale(1.05);
}

.btn-secondary {
  background-color: rgb(55, 65, 81);
  color: white;
  border-color: rgb(55, 65, 81);
}

.btn-secondary:hover {
  background-color: rgb(6, 182, 212);
  color: black;
  border-color: rgb(6, 182, 212);
}

.btn-outline {
  background-color: transparent;
  color: rgb(6, 182, 212);
  border-color: rgb(6, 182, 212);
}

.btn-outline:hover {
  background-color: rgb(6, 182, 212);
  color: black;
}

.btn-sm {
  padding: 0.5rem 1rem;
  font-size: 0.75rem;
}

.btn-lg {
  padding: 1rem 2rem;
}

.btn-disabled {
  opacity: 0.5;
  cursor: not-allowed;
}

.btn-loading {
  cursor: wait;
}

.btn:hover:not(.btn-disabled) {
  transform: scale(1.05);
}
</style>
