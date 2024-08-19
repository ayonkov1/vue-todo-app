<script setup lang="ts">
import { defineProps, defineEmits } from 'vue'

const props = defineProps(['todo', 'index'])
const emit = defineEmits(['remove'])

const removeTodo = () => {
  emit('remove', props.todo.id)
}
</script>

<template>
  <div>
    {{ index + 1 }}: {{ todo.title }}
    <span @click="removeTodo" style="cursor: pointer">❌</span>
  </div>
</template>
