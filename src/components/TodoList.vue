<script setup>
import List from './List.vue';
</script>

<script>
export default {
    components: {
        List,
    },
    props: {
        lists: {
            type: Array,
            required: true,
        },
    },
    methods: {
        updateForwardTodo(updatedTodo){
            this.$emit('updateTodo', updatedTodo)
        },

        removeFromLists(todoId){
            this.$emit('deleteTodo', todoId)
        }

    }
};
</script>
<template>
    <div class="mt-5 space-y-5 overflow-auto max-h-[50vh] pr-3">
        <List v-for="(list, index) in lists" :key="index" :data="list" @updateTodo="updateForwardTodo" @deleteTodo="removeFromLists"/>
    </div>
</template>