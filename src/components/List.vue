<script>
export default {
  props: {
    data: {
      type: Object,
      required: true,
    },
  },

  data() {
    return {
      newTodo: this.data.todo,
    };
  },

  methods: {
    handleTodoComplete(id) {
      this.$emit("updateTodo", {
        id: id,
        isCompleted: true,
      });
    },

    handleRemove(id) {
      this.$emit("deleteTodo", id);
    },

    handleEdit(id) {
      this.$emit("enableEdit", {
        id: id,
        isEdit: true,
      });
    },

    updateToNewTodo(e) {
      let inputValue = e.target.value;
      this.newTodo = inputValue.trim();
    },

    dispatchNewTodo(id) {
      this.$emit("updateNewTodo", {
        id: id,
        todo: this.newTodo,
        isEdit: false,
      });
    },
  },
};
</script>

<template>
  <div
    class="p-4 border border-gray-100 rounded-md"
    :class="{ 'bg-green-100': data.isCompleted }"
  >
    <div class="text-sm text-gray-600 flex justify-between items-center gap-5">
      <div
        class="break-words flex-1"
        :class="{ 'line-through': data.isCompleted }"
      >
        <form
          class="flex items-center gap-5 w-full"
          @submit.prevent="dispatchNewTodo(data.id)"
        >
          <input
            v-if="data.isEdit"
            type="text"
            name="new-todo"
            id="new-todo"
            class="block rounded-md bg-white w-full p-4 text-base text-gray-900 outline outline-1 -outline-offset-1 outline-gray-300 placeholder:text-gray-400 focus:outline focus:outline-2 focus:-outline-offset-2 focus:outline-[#42B883] sm:text-sm/6"
            :value="data.todo"
            @input="updateToNewTodo"
            :readonly="!data.isEdit"
          />
          <span class="block break-all" v-if="!data.isEdit">{{
            data.todo
          }}</span>
        </form>
      </div>
      <div class="inline-flex space-x-2">
        <button
          type="button"
          @click="handleTodoComplete(data.id)"
          title="Click to Complete"
          class="p-3 rounded-full transition-all duration-300 ease-in-out hover:bg-green-200 hover:text-green-600"
          :class="{ hidden: data.isCompleted }"
        >
          <svg
            xmlns="http://www.w3.org/2000/svg"
            fill="none"
            viewBox="0 0 24 24"
            stroke-width="2"
            stroke="currentColor"
            class="size-5"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              d="m4.5 12.75 6 6 9-13.5"
            />
          </svg>
        </button>
        <button
          type="button"
          @click="handleEdit(data.id)"
          title="Edit"
          class="p-3 rounded-full transition-all duration-300 ease-in-out hover:bg-blue-200 hover:text-blue-600"
          :class="{ hidden: data.isCompleted }"
        >
          <svg
            xmlns="http://www.w3.org/2000/svg"
            fill="none"
            viewBox="0 0 24 24"
            stroke-width="1.5"
            stroke="currentColor"
            class="size-5"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              d="m16.862 4.487 1.687-1.688a1.875 1.875 0 1 1 2.652 2.652L6.832 19.82a4.5 4.5 0 0 1-1.897 1.13l-2.685.8.8-2.685a4.5 4.5 0 0 1 1.13-1.897L16.863 4.487Zm0 0L19.5 7.125"
            />
          </svg>
        </button>
        <button
          type="button"
          @click="handleRemove(data.id)"
          title="Remove"
          class="p-3 rounded-full transition-all duration-300 ease-in-out hover:bg-red-200 hover:text-red-600"
        >
          <svg
            xmlns="http://www.w3.org/2000/svg"
            fill="none"
            viewBox="0 0 24 24"
            stroke-width="1.5"
            stroke="currentColor"
            class="size-5"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              d="m14.74 9-.346 9m-4.788 0L9.26 9m9.968-3.21c.342.052.682.107 1.022.166m-1.022-.165L18.16 19.673a2.25 2.25 0 0 1-2.244 2.077H8.084a2.25 2.25 0 0 1-2.244-2.077L4.772 5.79m14.456 0a48.108 48.108 0 0 0-3.478-.397m-12 .562c.34-.059.68-.114 1.022-.165m0 0a48.11 48.11 0 0 1 3.478-.397m7.5 0v-.916c0-1.18-.91-2.164-2.09-2.201a51.964 51.964 0 0 0-3.32 0c-1.18.037-2.09 1.022-2.09 2.201v.916m7.5 0a48.667 48.667 0 0 0-7.5 0"
            />
          </svg>
        </button>
      </div>
    </div>
  </div>
</template>
