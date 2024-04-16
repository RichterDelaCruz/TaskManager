<template>
    <li class="list-group-item d-flex justify-content-between align-items-center">
        <div>
            <span>{{ task.title }} - {{ task.status }}</span>
        </div>
        <div>
            <!-- Button to toggle task status -->
            <button @click="toggleStatus" class="btn btn-sm btn-primary me-2">Toggle Status</button>
            <button @click="deleteTask" class="btn btn-sm btn-danger">Delete</button>
        </div>
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
            // Toggle between 'pending' and 'completed' statuses
            const newStatus = this.task.status === 'pending' ? 'completed' : 'pending';
            // Emit event to update task status
            this.$emit('update-status', { id: this.task.id, status: newStatus });
        },
        deleteTask() {
            // Emit event to delete task
            this.$emit('delete-task', this.task.id);
        }
    }
}
</script>
