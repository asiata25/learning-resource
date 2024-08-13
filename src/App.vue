<script setup>
import { provide, ref, computed } from 'vue'
import AddResources from './components/learning-resources/AddResources.vue'
import StoredResources from './components/learning-resources/StoredResources.vue'
import BaseButton from './components/UI/BaseButton.vue'
import CardContainer from './components/UI/CardContainer.vue'

const storedResources = ref([
  {
    id: 'official-guide',
    title: 'Official Guide',
    note: 'Possimus tempore itaque voluptatibus amet earum ullam odit possimus illum.',
    link: 'https://vuejs.org/guide/introduction.html'
  },
  {
    id: 'google',
    title: 'Google',
    note: 'Numquam delectus maxime reprehenderit assumenda dolor sed iusto repellendus.',
    link: 'https://google.com'
  }
])
const addResources = (resource) => {
  const newResource = {
    id: new Date().toISOString(),
    title: resource.title,
    note: resource.note,
    link: resource.link
  }

  storedResources.value.unshift(newResource)
  activeTab.value = 'StoredResources'
}
provide('resources', { storedResources, addResources })
const activeTab = ref('StoredResources')
const tab = {
  StoredResources,
  AddResources
}

const onSwitchTab = (nameComponent) => {
  activeTab.value = nameComponent
}

const storedResButtonMode = computed(() => {
  return activeTab.value === 'StoredResources'
})
const addResButtonMode = computed(() => {
  return activeTab.value === 'AddResources'
})
</script>

<template>
  <div class="container py-4">
    <CardContainer class="shadow mb-5">
      <div class="btn-group w-100" role="group" aria-label="Basic example">
        <BaseButton :isActive="storedResButtonMode" @click="onSwitchTab('StoredResources')"
          >Stored Resources</BaseButton
        >
        <BaseButton :isActive="addResButtonMode" @click="onSwitchTab('AddResources')"
          >Add New</BaseButton
        >
      </div>
    </CardContainer>
    <KeepAlive>
      <component :is="tab[activeTab]"></component>
    </KeepAlive>
  </div>
</template>
