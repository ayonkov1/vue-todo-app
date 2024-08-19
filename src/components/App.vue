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

  todos.push({
    title: textInput.value,
    completed: false
  })
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
    <div v-for="(todo, index) of todos" :key="index">
      {{ todo.title }}
      <span @click="removeTodo(todo.title)" style="cursor: pointer">❌</span>
    </div>
  </header>

  <main>
    <input type="text" @input="onChangeHandler" />
    <button @click="onClickHandler">Add ToDo</button>
  </main>
</template>
