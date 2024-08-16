<script setup lang="ts">
import { RouterLink, RouterView } from 'vue-router'
import { useMessageStore } from './stores/message'
import { storeToRefs } from 'pinia'

const store = useMessageStore()
const { message } = storeToRefs(store)
</script>

<template>
  <div class="text-center font-sans text-gray-700 antialias">
    <header>
      <div id="flashMessage" class="animate-fade" v-if="message">
        <h4>{{ message }}</h4>
      </div>
      <div class="wrapper">
        <HelloWorld msg="You did it!" />

        <nav class="py-6 text-[20px]">
          <RouterLink class="font-bold text-gray-700" :to="{ name: 'event-list-view' }"
            >Event</RouterLink
          >
          | <RouterLink class="font-bold text-gray-700" :to="{ name: 'about' }">About</RouterLink> |
          <RouterLink class="font-bold text-gray-700" :to="{ name: 'student' }">student</RouterLink>
        </nav>
      </div>
    </header>
    <RouterView />
  </div>
</template>
