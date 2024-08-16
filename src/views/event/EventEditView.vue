<script setup lang="ts">
import type { Event } from '@/type'
import { toRefs } from 'vue'
import { useRouter } from 'vue-router'
import { useMessageStore } from '@/stores/message'

const props = defineProps<{
  event: Event
}>()
const { event } = toRefs(props)
const router = useRouter()
const store = useMessageStore()
const edit = () => {
  store.updateMessage('You are successfully updating the data for ' + props.event.title)
  setTimeout(() => {
    store.resetMessage()
  }, 3000)
  router.push({ name: 'event-detail-view', params: { id: props.event.id } })
}
</script>

<template>
  <button
    @click="edit"
    class="bg-gray-500 hover:bg-pink-700 text-white font-bold py-2 px-4 rounded"
  >
    Edit
  </button>
</template>
