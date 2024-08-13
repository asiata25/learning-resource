<script setup>
defineEmits(['closeModal'])
</script>

<template>
  <div class="position-absolute top-0 bottom-0 end-0 start-0 z-1 bg-dark bg-opacity-50"></div>
  <dialog class="card shadow-lg position-absolute p-0 top-50 start-50 translate-middle z-2">
    <div class="card-header">Featured</div>
    <div class="card-body">
      <h5 class="card-title">Special title treatment</h5>
      <p class="card-text">
        With supporting text below as a natural lead-in to additional content.
      </p>
    </div>
    <div class="card-footer text-body-secondary">
      <slot name="footer">
        <button class="btn btn-primary" @click="$emit('closeModal')">Close</button>
      </slot>
    </div>
  </dialog>
</template>
