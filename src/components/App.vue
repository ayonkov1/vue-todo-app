<script setup lang="ts">
import { reactive } from 'vue'

import TodoList from './Todo/TodoList.vue'
import TodoInput from './Todo/TodoInput.vue'

const todos = reactive([
  { title: 'Buy groceries', completed: false },
  { title: 'Finish project report', completed: false }
])

const addTodo = (title: string) => {
  todos.push({ title, completed: false })
}

const removeTodo = (title: string) => {
  const index = todos.findIndex((todo) => todo.title === title)
  if (index > -1) todos.splice(index, 1)
}

const resetTodos = () => {
  while (todos.length) todos.pop()
}
</script>

<template>
  <div class="flex flex-col gap-10 min-w-[80vw] h-[60vh] lg:flex-row">
    <header class="flex-1 border rounded-lg">
      <TodoList :todos="todos" @remove="removeTodo" />
    </header>
    <main class="flex-1">
      <TodoInput @add="addTodo" @reset="resetTodos" />
    </main>
  </div>
</template>
