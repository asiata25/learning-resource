<script setup lang="ts">
import { computed } from 'vue'
export interface Props {
  variant?: 'primary' | 'danger'
  isActive?: boolean
}

const props = withDefaults(defineProps<Props>(), {
  variant: 'primary',
  isActive: false
})

const btnClass = computed(() => {
  let classBtn = 'btn '
  if (props.variant === 'primary' && props.isActive) {
    classBtn += ' btn-primary active'
  } else if (props.variant === 'primary' && !props.isActive) {
    classBtn += ' btn-outline-primary'
  }

  if (props.variant === 'danger') {
    classBtn += ' btn-link text-danger text-decoration-none'
  }

  return classBtn
})
</script>

<template>
  <button type="button" :class="btnClass"><slot></slot></button>
</template>
