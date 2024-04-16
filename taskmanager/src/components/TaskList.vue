<template>
    <div class="container">
        <div class="row justify-content-center mt-5">
            <div class="col-md-6">
                <h2>Tasks</h2>
                <ul>
                    <TaskItem v-for="task in tasks" :key="task.id" :task="task" @update-status="updateTaskStatus"
                        @delete-task="deleteTask" class="my-2" />
                </ul>
            </div>
        </div>
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
            this.$emit('update-status', taskId);
        },
        deleteTask(taskId) {
            this.$emit('delete-task', taskId);
        }
    }
}
</script>