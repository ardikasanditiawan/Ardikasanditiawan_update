<template>
    <form @submit.prevent="handleSubmit" class="task-form">
      <input
        type="text"
        placeholder="I need to..."
        v-model="newTask"
        class="task-input"
      />
      <button class="add-button">Add</button>
    </form>
  </template>
  
  <script>
  import { useTaskStore } from '@/stores/TaskStore';
  import { ref } from 'vue';
  
  export default {
    setup() {
      const taskStore = useTaskStore();
      const newTask = ref('');
  
      const handleSubmit = () => {
        if (newTask.value.length > 0) {
          taskStore.addTask({
            title: newTask.value,
            isFav: false,
            id: Math.floor(Math.random() * 10000)
          });
          newTask.value = '';
        }
      };
  
      return { handleSubmit, newTask };
    }
  }
  </script>
  
  <style scoped>
  .task-form {
    display: flex;
    align-items: center;
    justify-content: center;
    margin-bottom: 25px;
  }
  
  .task-input {
    padding: 8px;
    font-size: 16px;
    border: 1px solid #ccc;
    border-radius: 4px;
  }
  
  .add-button {
  padding: 16px;
  font-size: 14px;
  font-weight: bold;
  color: #fff;
  background-color: rgb(255, 0, 0);
  border: none;
  border-radius: 4px;
  cursor: pointer;
}
  </style>
  