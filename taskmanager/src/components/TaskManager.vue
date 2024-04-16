<template>
    <div>
        <TaskForm @add-task="addTaskToServer" />
        <TaskList :tasks="tasks" @update-status="updateTaskStatusOnServer" @delete-task="deleteTaskFromServer" />
    </div>
</template>

<script>
import axios from 'axios';
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
            tasks: []
        };
    },
    mounted() {
        // Fetch tasks from the server when the component is mounted
        this.fetchTasksFromServer();
    },
    methods: {
        async fetchTasksFromServer() {
            try {
                const response = await axios.get('http://localhost:3000/tasks');
                this.tasks = response.data;
            } catch (error) {
                console.error('Error fetching tasks:', error);
            }
        },
        async addTaskToServer(newTask) {
            try {
                await axios.post('http://localhost:3000/tasks', newTask);
                // After adding task to server, fetch updated tasks from server
                this.fetchTasksFromServer();
            } catch (error) {
                console.error('Error adding task:', error);
            }
        },
        async updateTaskStatusOnServer(updatedTask) {
            try {
                await axios.put(`http://localhost:3000/tasks/${updatedTask.id}`, { status: updatedTask.status });
                // After updating task status on server, fetch updated tasks from server
                this.fetchTasksFromServer();
            } catch (error) {
                console.error('Error updating task status:', error);
            }
        },
        async deleteTaskFromServer(taskId) {
            try {
                await axios.delete(`http://localhost:3000/tasks/${taskId}`);
                // After deleting task from server, fetch updated tasks from server
                this.fetchTasksFromServer();
            } catch (error) {
                console.error('Error deleting task:', error);
            }
        }
    }
};
</script>
