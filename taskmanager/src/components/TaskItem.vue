<template>
    <li>
        <span>{{ task.title }} - {{ task.status }}</span>
        <button @click="toggleStatus">Toggle Status</button>
        <button @click="deleteTask">Delete</button>
    </li>
</template>

<script>
export default {
    name: 'TaskItem',
    props: {
        task: {
            type: Object,
            required: true
        }
    },
    methods: {
        toggleStatus() {
            // Emit an event to the parent component to update the task status
            this.$emit('update-status', this.task.id); // Pass task id instead of the whole task
        },
        deleteTask() {
            // Emit an event to the parent component to delete the task
            this.$emit('delete-task', this.task.id); // Pass task id instead of the whole task
        }
    }
}
</script>