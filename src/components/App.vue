<script setup lang="ts">
import { ref } from 'vue'

const input = ref(1)
const textInput = ref('')

const increment = () => {
  input.value++
}

const onChangeHandler = (event: any) => {
  if (event) {
    event.preventDefault()
  }
  textInput.value = event.target.value
}
</script>

<template>
  <header>
    <div class="wrapper">Counter: {{ input }}</div>
    <button @click="increment">Increase count</button>
  </header>

  <main>
    <input type="text" @input="onChangeHandler" />
    <div>{{ textInput }}</div>
  </main>
</template>
