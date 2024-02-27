<script setup>
import { ref } from 'vue';
import EditForm from './EditForm.vue';

const tasks = ref([
  { name: 'Task 1', time: 30 },
  { name: 'Task 2', time: 40 },
  { name: 'Task 3', time: 60 },
  { name: 'Task 4', time: 45 },
  { name: 'Task 5', time: 50 },
]);


let isFormVisible = ref(false);
let editIndex = ref(null);

const openEditForm = (index) => {
  isFormVisible.value = true;
  editIndex.value = index;
};

const closeForm = () => {
  isFormVisible.value = false;
  editIndex.value = null;
};

const updateTask = (updatedTask) => {
    if (updatedTask.time === 0) {
    // Show an alert if the user tries to update time to 0 minutes
    alert("Time cannot be 0 minutes. Please enter a valid time.");
  } else {
    tasks.value[editIndex.value] = { ...updatedTask };
    isFormVisible.value = false;
    editIndex.value = null;
  }
};
</script>

<template>

    <div class="border rounded-md mt-12 flex flex-col p-5 mx-auto max-w-[400px] px-4 sm:px-6 lg:px-8 relative min-h-[300px]">
        <h1 class="text-3xl font-bold mb-5 text-center border-b-[1px] pb-3 border-blue-300">
            Task List
        </h1>
        <div>
            <div class="flex gap-3 items-center mb-5 justify-between" v-for="(task, index) in tasks" :key="index">
                <span class="text-2xl font-bold">{{ task.name }} - {{ task.time }} {{ task.time > 1 ? "Minutes": "Minute" }}</span>
                <button class="text-blue-500 px-0 py-0 mt-[5px] rounded-md" @click="openEditForm(index)">
                    <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-6 h-6">
                        <path stroke-linecap="round" stroke-linejoin="round" d="m16.862 4.487 1.687-1.688a1.875 1.875 0 1 1 2.652 2.652L10.582 16.07a4.5 4.5 0 0 1-1.897 1.13L6 18l.8-2.685a4.5 4.5 0 0 1 1.13-1.897l8.932-8.931Zm0 0L19.5 7.125M18 14v4.75A2.25 2.25 0 0 1 15.75 21H5.25A2.25 2.25 0 0 1 3 18.75V8.25A2.25 2.25 0 0 1 5.25 6H10" />
                    </svg>
                </button>
            </div>
        </div>

    <EditForm
      v-if="isFormVisible"
      :task="tasks[editIndex]"
      @submit="updateTask"
      @close="closeForm"
    />
  </div>
</template>

<style scoped>

</style>
