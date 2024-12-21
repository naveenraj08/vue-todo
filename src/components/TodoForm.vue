<script>
export default {
  data() {
    return {
      todoValue: "",
    };
  },
  methods: {
    onInput(e) {
      let inputValue = e.target.value;
      this.todoValue = inputValue.trim();
    },
    dispatchTodo() {
      if (this.todoValue) {
        this.$emit("todoListItem", {
          id: Math.random().toString(36).substr(2, 9),
          todo: this.todoValue,
          isCompleted: false,
          isEdit: false,
        });
        this.todoValue = "";
      }
    },
  },
};
</script>

<template>
  <form class="flex items-center gap-5" @submit.prevent="dispatchTodo">
    <input
      type="text"
      name="username"
      id="username"
      class="block flex-1 rounded-md bg-white p-4 text-base text-gray-900 outline outline-1 -outline-offset-1 outline-gray-300 placeholder:text-gray-400 focus:outline focus:outline-2 focus:-outline-offset-2 focus:outline-[#42B883] sm:text-sm/6"
      placeholder="What's on your mind?"
      :value="todoValue"
      @input="onInput"
    />
    <button
      type="submit"
      class="rounded-md p-4 text-sm font-semibold text-white shadow-sm hover:bg-[#42B883] focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-[#42B883] bg-[#42B883]"
    >
      Add
    </button>
  </form>
</template>
