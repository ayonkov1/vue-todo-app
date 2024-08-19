<script setup lang="ts">
import { reactive, ref } from 'vue'

const todos = reactive([
  {
    title: 'Buy groceries',
    completed: false
  },
  {
    title: 'Finish project report',
    completed: false
  }
])
const textInput = ref('')

const onClickHandler = (event: any) => {
  if (event) {
    event.preventDefault()
  }

  if (textInput.value.trim() === '') return
  todos.push({
    title: textInput.value,
    completed: false
  })

  textInput.value = ''
}

const onChangeHandler = (event: any) => {
  textInput.value = event.target.value
}

const removeTodo = (title: string) => {
  // todos = todos.filter((todo) => todo.title !== title)     -- in case we go for ref
  var index = todos.findIndex((todo) => todo.title === title)
  todos.splice(index, 1)
}
</script>

<template>
  <header>
    <div v-for="(item, index) of todos" :key="index">
      {{ index + 1 }}: {{ item.title }}
      <span @click="removeTodo(item.title)" style="cursor: pointer">❌</span>
    </div>
  </header>

  <main class="flex gap-4 h-8">
    <input class="border rounded-lg p-1" type="text" v-model="textInput" @input="onChangeHandler" />
    <button class="border rounded-lg p-1" @click="onClickHandler">Add ToDo</button>
  </main>
</template>
