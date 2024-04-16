<template>
    <div>
        <h2>Add Task</h2>
        <form @submit.prevent="addTask">
            <label>Title:</label>
            <input type="text" v-model="title" required>
            <label>Status:</label>
            <input type="text" v-model="status" required>
            <button type="submit">Add Task</button>
        </form>
    </div>
</template>

<script>
export default {
    name: 'TaskForm',
    data() {
        return {
            title: '',
            status: ''
        };
    },
    methods: {
        addTask() {
            // Generate a unique identifier for the task
            const taskId = Math.random().toString(36).substr(2, 9); // Example of generating a random ID
            // Emit an event to the parent component to add the task with the generated ID
            this.$emit('add-task', { id: taskId, title: this.title, status: this.status });
            // Clear the form fields after adding the task
            this.title = '';
            this.status = '';
        }
    }
}
</script>