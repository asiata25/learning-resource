<script setup lang="ts">
import CardContainer from '../UI/CardContainer.vue'

defineProps({
  title: {
    type: String,
    required: true
  },
  note: {
    type: String,
    required: true
  },
  link: {
    type: String,
    required: true
  }
})
</script>

<template>
  <CardContainer>
    <template v-slot:header>
      <div class="title">
        <h5>{{ title }}</h5>
        <button type="button" class="btn btn-link text-danger text-decoration-none">Delete</button>
      </div>
    </template>
    <slot>
      <p class="card-text">
        {{ note }}
      </p>
    </slot>
    <template v-slot:footer>
      <a :href="link" target="_blank" class="card-link">Resource Link</a>
    </template>
  </CardContainer>
</template>

<style scoped lang="scss">
.title {
  display: flex;
  align-items: center;
  justify-content: space-between;

  h5 {
    margin-bottom: 0px;
  }
}
</style>
