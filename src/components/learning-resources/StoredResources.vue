<script setup lang="ts">
import LearningResource from './LearningResource.vue'
import { inject } from 'vue'

const resourcesState = inject<{
  storedResources: { id: string; title: string; note: string; link: string }[]
}>('resources')

const { storedResources: resources } = resourcesState!
</script>

<template>
  <div class="row row-gap-3">
    <div class="col-12" v-for="resource in resources" :key="resource.id">
      <LearningResource :title="resource.title" :note="resource.note" :link="resource.link" />
    </div>
  </div>
</template>
