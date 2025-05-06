<template>
  <div class="container mt-5">
    <h2 class="text-center mb-4">Vue Todo App</h2>
    <TodoApp />
  </div>
</template>

<script>
import TodoApp from '@/components/ToDoApp.vue'

export default {
  components: {
    TodoApp
  }
}
</script>
