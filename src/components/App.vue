<script setup lang="ts">
import { reactive } from 'vue'
import { Toaster, toast } from '@steveyuowo/vue-hot-toast'
import '@steveyuowo/vue-hot-toast/vue-hot-toast.css'

import TodoList from './Todo/TodoList.vue'
import TodoInput from './Todo/TodoInput.vue'

const todos = reactive([
  { id: 1, title: 'Buy groceries', completed: false },
  { id: 2, title: 'Finish project report', completed: false }
])

const addTodo = (title: string) => {
  todos.push({ id: todos.length + 1, title, completed: false })
}

const removeTodo = (id: number) => {
  const index = todos.findIndex((todo) => todo.id === id)
  if (index > -1) todos.splice(index, 1)
  toast.success(`Todo Nr. ${index + 1} removed!`)
}

const resetTodos = () => {
  if (!todos.length) {
    toast.error('List already empty!')
    return
  }
  const id = toast.loading('Loading...')
  setTimeout(() => {
    while (todos.length) todos.pop()
    toast.update(id, {
      type: 'success',
      message: 'Removed todo items!',
      duration: 1000
    })
  }, 500)
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
  <Toaster />
</template>
