<script setup lang="ts">
import { ref, defineEmits } from 'vue'

const textInput = ref('')
const emit = defineEmits(['add', 'reset'])

const addTodo = () => {
  if (textInput.value.trim() === '') return
  emit('add', textInput.value)
  textInput.value = ''
}

const resetTodos = () => {
  emit('reset')
}
</script>

<template>
  <div class="flex gap-4">
    <div class="flex flex-col flex-grow gap-4 lg:flex-row">
      <input
        class="border-slate-800 border rounded-lg p-4 flex-grow"
        type="text"
        v-model="textInput"
        placeholder="Write a Todo here..."
        @keyup.enter="addTodo"
      />

      <button class="border rounded-lg p-4" @click="addTodo">Add ToDo</button>
      <button class="border rounded-lg p-4" @click="resetTodos">Reset</button>
    </div>
  </div>
</template>
