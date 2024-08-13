<script setup lang="ts">
import { inject, ref, type Ref } from 'vue'
import BaseModal from '../UI/BaseModal.vue'

const inputTitle = ref<HTMLInputElement | null>(null)
const inputNote = ref<HTMLInputElement | null>(null)
const inputLink = ref<HTMLInputElement | null>(null)

const isModalOpen: Ref<boolean> = ref(false)

const resourcesState = inject<{
  addResources: (resource: { title: string; note: string; link: string }) => void
}>('resources')

const { addResources } = resourcesState!

const onSubmit = () => {
  if (
    inputTitle.value!.value.trim() === '' ||
    inputNote.value!.value.trim() === '' ||
    inputLink.value!.value.trim() === ''
  ) {
    isModalOpen.value = true
    return
  }

  addResources({
    title: inputTitle.value!.value,
    note: inputNote.value!.value,
    link: inputLink.value!.value
  })
}

const onCloseModal = () => {
  isModalOpen.value = false
}
</script>

<template>
  <Teleport to="body">
    <BaseModal v-if="isModalOpen" @close-modal="onCloseModal">
      <template #footer>
        <button class="btn btn-danger" @click="onCloseModal">Close</button>
      </template>
    </BaseModal>
  </Teleport>
  <form @submit.prevent="onSubmit">
    <div class="mb-3">
      <label for="title" class="form-label">Title</label>
      <input
        type="text"
        class="form-control"
        id="title"
        aria-describedby="title"
        ref="inputTitle"
      />
    </div>
    <div class="mb-3">
      <label for="note" class="form-label">Note</label>
      <textarea class="form-control" id="note" rows="3" ref="inputNote"></textarea>
    </div>
    <div class="mb-3">
      <label for="link" class="form-label">Link</label>
      <input type="text" class="form-control" id="link" aria-describedby="link" ref="inputLink" />
    </div>
    <button type="submit" class="btn btn-primary">Submit</button>
  </form>
</template>
