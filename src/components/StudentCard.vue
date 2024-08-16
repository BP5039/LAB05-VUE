<script setup lang="ts">
import type { Student } from '@/type'
defineProps<{
  student: Student
}>()
</script>

<template>
  <div class="student-class">
    <div
      class="student-card p-5 w-64 cursor-pointer border border-gray-700 mb-4 hover:scale-105 hover:shadow-lg transition-transform duration-200"
    >
      <h2>{{ student.name + ' ' + student.surname }}</h2>
      <h2>GPA: {{ student.gpa }}</h2>
    </div>
  </div>
</template>

<style scoped></style>
