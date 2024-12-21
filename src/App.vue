<script setup>
import TodoForm from "./components/TodoForm.vue";
import TodoList from "./components/TodoList.vue";
</script>

<script>
export default {
  components: {
    TodoForm,
    TodoList,
  },

  data() {
    return {
      todoLists: [],
    };
  },

  methods: {
    handleChildData(data) {
      this.todoLists = [...this.todoLists, data];
    },

    markTodoComplete(status) {
      let locateIndex = this.todoLists.findIndex(
        (todo) => todo.id === status.id
      );
      if (locateIndex !== -1) {
        this.todoLists[locateIndex].isCompleted = status.isCompleted;
      }
    },

    editTodo(newTodo) {
      let locateIndex = this.todoLists.findIndex(
        (todo) => todo.id === newTodo.id
      );
      if (locateIndex !== -1) {
        if (!newTodo.isEdit) {
          this.todoLists[locateIndex].isEdit = newTodo.isEdit;
          this.todoLists[locateIndex].todo = newTodo.todo;
        } else {
          this.todoLists[locateIndex].isEdit = newTodo.isEdit;
        }
      }
    },

    removeFromLists(id) {
      const newList = this.todoLists.filter((todo) => todo.id !== id);
      this.todoLists = newList;
    },
  },
};
</script>

<template>
  <div class="container mx-auto py-10">
    <h1 class="text-center text-2xl font-medium">
      Todo with Vite + Vue 3 + TailwindCSS
    </h1>
    <div class="card my-10 max-w-lg mx-auto">
      <TodoForm @todoListItem="handleChildData" />
      <TodoList
        :lists="todoLists"
        @updateTodo="markTodoComplete"
        @deleteTodo="removeFromLists"
        @enableEdit="editTodo"
        @updateNewTodo="editTodo"
      />
    </div>
  </div>
</template>
