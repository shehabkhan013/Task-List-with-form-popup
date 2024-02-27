<script setup>
import { ref, defineProps, defineEmits } from 'vue';

const props = defineProps(['task']);
const emits = defineEmits(['submit', 'close']);

const editedTask = ref({ ...props.task });

const submitForm = () => {
  emits('submit', editedTask.value);
};

const closeForm = () => {
  emits('close');
};
</script>

<template>
   <div class="edit-form absolute w-full h-full flex flex-col justify-center items-center bg-white top-0 left-0 p-5">
    <h2 class="text-3xl font-bold mb-5 text-center">
        Edit Task 
    </h2>
    <form @submit.prevent="submitForm">
      <input class="mb-3 border-[1px] w-full h-[50px] px-4 focus:border-blue-500 focus-visible:border-blue-500 focus:outline-none" v-model="editedTask.name" type="text" placeholder="Task Name" />
      <input class="mb-3 border-[1px] w-full h-[50px] px-4 focus:border-blue-500 focus-visible:border-blue-500 focus:outline-none" v-model="editedTask.time" type="number" placeholder="Task Time" />
      <button class="bg-blue-500 text-white px-3 py-3 rounded-md w-full" type="submit">Update Task</button>
    </form>
    <button class="text-red-500 bg-white px-0 py-0 mt-[5px] rounded-md absolute top-[-14px] right-[-13px]" @click="closeForm"><svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-6 h-6">
  <path stroke-linecap="round" stroke-linejoin="round" d="m9.75 9.75 4.5 4.5m0-4.5-4.5 4.5M21 12a9 9 0 1 1-18 0 9 9 0 0 1 18 0Z" />
</svg></button>
  </div>
</template>



<style scoped>

</style>