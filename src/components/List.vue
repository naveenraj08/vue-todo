<script>
export default {
    props: {
        data: {
            type: Object, // or the appropriate type based on your data
            required: true,
        },
    },
};
</script>

<template>
    <div class="p-4 border border-gray-100 rounded-md">
        <div class="text-sm text-gray-600">{{ data }}</div>
    </div>
</template>