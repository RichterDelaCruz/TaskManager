<template>
    <div>
        <TaskForm @add-task="addTask" />
        <TaskList :tasks="tasks" @update-status="updateTaskStatus" @delete-task="deleteTask" />
    </div>
</template>

<script>
import TaskForm from './TaskForm.vue';
import TaskList from './TaskList.vue';

export default {
    name: 'TaskManager',
    components: {
        TaskForm,
        TaskList
    },
    data() {
        return {
            tasks: [] // Assuming this is an array of tasks fetched from the API
        };
    },
    methods: {
        addTask(newTask) {
            // Add the new task to the tasks array
            this.tasks.push(newTask);
            // You would also send a POST request to your backend API to add the task
        },
        updateTaskStatus(taskId) {
            // Find the index of the task to update
            const index = this.tasks.findIndex(task => task.id === taskId);
            // Toggle the status of the task
            this.tasks[index].status = this.tasks[index].status === 'completed' ? 'pending' : 'completed';
            // You would also send a PUT request to your backend API to update the task status
        },
        deleteTask(taskId) {
            // Filter out the task to delete from the tasks array
            this.tasks = this.tasks.filter(task => task.id !== taskId);
            // You would also send a DELETE request to your backend API to delete the task
        }
    }
}
</script>