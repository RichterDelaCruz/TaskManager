<template>
    <div>
        <h2>Tasks</h2>
        <ul>
            <TaskItem v-for="task in tasks" :key="task.id" :task="task" @update-status="updateTaskStatus"
                @delete-task="deleteTask" />
        </ul>
    </div>
</template>

<script>
import TaskItem from './TaskItem.vue';

export default {
    name: 'TaskList',
    components: {
        TaskItem
    },
    props: {
        tasks: {
            type: Array,
            required: true
        }
    },
    methods: {
        updateTaskStatus(taskId) {
            // Emit an event to the parent component to update the task status
            this.$emit('update-status', taskId);
        },
        deleteTask(taskId) {
            // Emit an event to the parent component to delete the task
            this.$emit('delete-task', taskId);
        }
    }
}
</script>