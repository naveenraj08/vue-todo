<script setup>
import List from './List.vue';
</script>

<script>
export default {
    components: {
        List,
    },
    mounted() {
        console.log('Message from parent:', this.lists);
    },
    props: {
        lists: Array, // Define the type of the prop
    },
};
</script>
<template>
    <div class="mt-5 overflow-auto max-h-[50vh]">
        <List v-for="(list, index) in lists" :key="index" :data="item" />
    </div>
</template>