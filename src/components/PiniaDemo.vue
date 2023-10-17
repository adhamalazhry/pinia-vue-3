<template>
  <header class="header">
    <div class="header-content">
      <img src="/public/logo.svg" alt="pinia logo" class="logo" />
      <p class="name">pinia tasks</p>
    </div>
    <div>
      <TaskFormVue />
    </div>
  </header>

  <nav class="filter">
    <button
      @click="filter = 'all'"
      class="filter-button"
      :class="{ active: filter === 'all' }"
    >
      All tasks
    </button>
    <button
      @click="filter = 'favs'"
      class="filter-button"
      :class="{ active: filter === 'favs' }"
    >
      Fav tasks
    </button>
    <button class="reset" @click="taskStore.$reset"> reset</button>
  </nav>
  <div class="loading" v-if="loading">
    <span class="material-symbols-outlined">
      refresh
      </span>
    loading tasks....
  </div>
  <div class="task-list" v-if="filter === 'all'">
    <p>your have {{ totalCount }} tasks left to do</p>
    <div v-for="task in tasks" :key="task.id">
      <TaskDetails :task="task" />
    </div>
  </div>
  <div class="task-list" v-if="filter === 'favs'">
    <p>your have {{ favCount }} favs left to do</p>
    <div v-for="task in favs" :key="task.id">
      <TaskDetails :task="task" />
    </div>
  
  </div>
 
</template>

<script>
import {storeToRefs} from 'pinia'
import TaskDetails from "./TaskDetails.vue";
import TaskFormVue from "./TaskForm.vue";
import { useTaskStore } from "../stores/TaskStore";
import { ref } from "vue";

export default {
  components: {
    TaskDetails,
    TaskFormVue,
  },
  setup() {
  const taskStore = useTaskStore();
  const {tasks,loading,favs,totalCount,favCount}=storeToRefs(taskStore)
  taskStore.getTasks()
  const deleteTask = (taskId) => {
    taskStore.deleteTask(taskId);
  };
  const filter = ref("all");
  return { taskStore, filter, deleteTask,tasks,loading,favs,totalCount,favCount };
},
};
</script>

<style scoped>
.header {
  background-color: #007bff;
  color: white;
  padding: 10px 20px;
}

.header-content {
  display: flex;
  align-items: center;
  justify-content: center;
}

/* Add styles for the loading indicator */
.loading {
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 10px;
  font-size: 18px;
  background-color: #f0f0f0;
}
.task-list {
  max-width: 50%;
  margin: 20px auto;
}
.logo {
  width: 50px;
  height: 50px;
  margin-right: 10px;
}

.name {
  font-size: 18px;
  font-weight: bold;
}

.filter {
  margin-left: 60%;
}

.filter-button {
  display: inline-block;
  background-color: #007bff;
  color: white;
  padding: 10px 20px;
  border: none;
  cursor: pointer;
  margin: 5px;
  border-radius: 5px;
  margin-left: 7px;
}

.filter-button.active {
  background-color: #0056b3; /* Darker shade when active */
}
.reset{
  background-color: #201e24b6;
  color: white;
  padding: 10px 20px;
  border: none;
  cursor: pointer;
  margin: 5px;
  border-radius: 5px;
  margin-left: 7px;
}

.material-symbols-outlined {
  font-variation-settings:
    'FILL' 1,
    'wght' 700,
    'GRAD' 200,
    'opsz' 20;
}
.loading {
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 10px;
  font-size: 18px;
  background-color: #f0f0f0;
  transition: opacity 0.3s, transform 0.3s;
  opacity: 1;
  transform: translateY(0);
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: 9999;
  /* Add more styles or animations as needed */
}
</style>
