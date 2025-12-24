<!-- eslint-disable vue/multi-word-component-names -->
<template>
  <div
    :class="[
      'card',
      variant === 'default' && 'card-default',
      variant === 'elevated' && 'card-elevated',
      variant === 'bordered' && 'card-bordered',
      hover && 'card-hover',
      'transition-all duration-300',
    ]"
  >
    <div v-if="$slots.header" class="card-header">
      <slot name="header" />
    </div>

    <div class="card-body">
      <slot />
    </div>

    <div v-if="$slots.footer" class="card-footer">
      <slot name="footer" />
    </div>
  </div>
</template>

<script setup lang="ts">
interface Props {
  variant?: 'default' | 'elevated' | 'bordered'
  hover?: boolean
}

withDefaults(defineProps<Props>(), {
  variant: 'default',
  hover: true,
})
</script>

<style scoped>
.card {
  background-color: rgb(17 24 39);
  border: 1px solid rgb(55 65 81);
  border-radius: 0.5rem;
  overflow: hidden;
  transition: all 0.3s;
}

.card-elevated {
  box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1);
}

.card-bordered {
  border-color: rgb(6 182 212);
}

.card-hover {
  cursor: pointer;
}

.card-hover:hover {
  border-color: rgb(6 182 212);
  transform: translateY(-2px);
  box-shadow: 0 0 20px rgba(6, 182, 212, 0.1);
}

.card-header {
  padding: 1rem 1.5rem;
  border-bottom: 1px solid rgb(55 65 81);
}

.card-body {
  padding: 1.5rem;
}

.card-footer {
  padding: 1rem 1.5rem;
  border-top: 1px solid rgb(55 65 81);
  background-color: rgb(55 65 81 / 0.5);
}
</style>
