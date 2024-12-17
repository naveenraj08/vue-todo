<script setup>
import TodoForm from './components/todoForm.vue';
import TodoList from './components/TodoList.vue';
</script>

<script>
export default {
  components: {
    TodoForm,
    TodoList
  },
  data() {
    return {
      todoLists: [],
    };
  },
  methods: {
    handleChildData(data) {
      this.todoLists = [...this.todoLists, data];
    }
  }
};
</script>

<template>
  <div class="container mx-auto py-10">
    <h1 class="text-center text-2xl font-medium">Todo with Vite + Vue 3 + TailwindCSS</h1>
    <div class="card my-10 max-w-md mx-auto">
      <TodoForm @todoListItem="handleChildData" />
      <TodoList :lists="todoLists" />
    </div>
  </div>
</template>