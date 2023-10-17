<template>
    <form @submit.prevent="handleSubmit">
      <label for="task">Task</label> <!-- افتراض اسم الحقل هو "Task" -->
      <input id="task" type="text" v-model="newTask" required />
      <button type="submit">Add Task</button>
    </form>
  </template>
  
  <script>
  import { useTaskStore } from "../stores/TaskStore";
  import { ref } from "vue";
  
  export default {
    setup() {
      const taskStore = useTaskStore(); // اسم المتغير يجب أن يكون taskStore، ليس tsakStore
      const newTask = ref("");
      
      const handleSubmit = () => {
        if (newTask.value.length > 0) {
          taskStore.addTask({
            title: newTask.value,
            isFav: false,
            id: Math.floor(Math.random() * 1000),
          });
          newTask.value = '';
        }
      }
      
      return { taskStore, newTask, handleSubmit };
    },
  };
  </script>
  <style scoped>
  form {
    display: flex;
    flex-direction: column;
    max-width: 300px;
    margin: 0 auto;
  }

  label {
    font-weight: bold;
    margin-bottom: 5px;
  }

  input {
    padding: 8px;
    margin-bottom: 10px;
    border: 1px solid #ccc;
    border-radius: 5px;
    font-size: 16px;
  }

  button {
    background-color: #909dac;
    color: white;
    padding: 10px;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    font-size: 16px;
  }

  button:hover {
    background-color: #09da14; /* تظلم لون زر عند التحويم */
  }
</style>

  