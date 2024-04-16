<template>
    <div class="container">
        <div class="row justify-content-center mt-5">
            <div class="col-md-6">
                <h2 class="mb-4">Add Task</h2>
                <form @submit.prevent="addTask" class="row align-items-center">
                    <div class="col">
                        <input type="text" id="title" class="form-control" v-model="title" required
                            placeholder="Task Name">
                    </div>
                    <div class="col">
                        <!-- Display status as text next to the title -->
                        <input type="text" v-model="status" class="form-control" value="pending" readonly>
                    </div>
                    <div class="col-auto">
                        <!-- Add Task button -->
                        <button type="submit" class="btn btn-primary">Add Task</button>
                    </div>
                </form>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'TaskForm',
    data() {
        return {
            title: '',
            status: 'pending' // Set the status to 'pending' by default
        };
    },
    methods: {
        addTask() {
            // Emit an event to the parent component to add the task with the generated ID
            this.$emit('add-task', { title: this.title, status: this.status });
            // Clear the form fields after adding the task
            this.title = '';
            // Leave the status as 'pending' without clearing it
        }
    }
}
</script>