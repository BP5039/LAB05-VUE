<script setup lang="ts">
import EventCard from '@/components/EventCard.vue'
import type { Event } from '@/type'
import { ref, onMounted, watchEffect, computed } from 'vue'
import EventService from '@/services/EventService'
import type { AxiosResponse } from 'axios'

const events = ref<Event[]>([])
const totalEvent = ref<number>(0)
const props = defineProps({
  page: {
    type: Number,
    required: true
  },
  eventsPerPage: {
    type: Number,
    required: true
  }
})

onMounted(() => {
  watchEffect(() => {
    EventService.getEvents(props.eventsPerPage, props.page).then(
      (response: AxiosResponse<Event[]>) => {
        events.value = response.data
        totalEvent.value = parseInt(response.headers['x-total-count'])
      }
    )
  })
})

const hasNextPage = computed(() => {
  const totalPages = Math.ceil(totalEvent.value / props.eventsPerPage)
  return props.page < totalPages && events.value.length > 0
})
</script>

<template>
  <h1>Event for good</h1>
  <div class="flex flex-col items-center">
    <EventCard v-for="event in events" :key="event.id" :event="event"></EventCard>
    <div class="flex w-72">
      <RouterLink
        :to="{ name: 'event-list-view', query: { page: page - 1 } }"
        rel="prev"
        v-if="page != 1"
        class="flex-1 text-left no-underline text-gray-800"
      >
        Prev Page
      </RouterLink>
      <RouterLink
        :to="{ name: 'event-list-view', query: { page: page + 1 } }"
        rel="next"
        v-if="hasNextPage"
        class="flex-1 text-right no-underline text-gray-800"
      >
        Next Page
      </RouterLink>
    </div>
  </div>
</template>

<style scoped></style>
