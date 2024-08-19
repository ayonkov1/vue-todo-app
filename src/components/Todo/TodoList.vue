<script setup lang="ts">
import { defineProps, defineEmits } from 'vue'
import TodoItem from './TodoItem.vue'

defineProps(['todos'])
const emit = defineEmits(['remove'])

const handleRemove = (title: string) => {
  emit('remove', title)
}
</script>

<template>
  <div class="max-h-full p-4 overflow-scroll">
    <div v-if="!todos.length">Empty</div>

    <div v-else>
      <TodoItem
        v-for="(todo, index) in todos"
        :key="index"
        :todo="todo"
        :index="index"
        @remove="handleRemove"
      />
    </div>
  </div>
</template>
