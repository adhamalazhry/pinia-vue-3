<template>
  <div class="task">
    <h3 class="task-title">{{ task.title }}</h3>
    <div class="icons">
      <i
        class="material-symbols-outlined"
        @click="taskStore.delete(task.id)"
        >delete</i
      >

      <i 
      class="material-symbols-outlined"
      :class="{active:task.isFav}"
      @click="taskStore.toggleFav(task.id)"
      >favorite</i>
    </div>
  </div>
</template>

<script>
import { useTaskStore } from "../stores/TaskStore";

export default {
  props: ["task"],
  setup() {
    const taskStore = useTaskStore();

    return { taskStore };
  },
};
</script>

<style scoped>
.task {
  border: 1px solid #ccc;
  padding: 6px 20px;
  margin-top: 10px;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.task-title {
  font-size: 18px;
  font-weight: bold;
}

.icons {
  display: flex;
  font-size: 24px;
  gap: 10px;
  cursor: pointer;
}
.icons i.active {
    color: red;
}


.material-symbols-outlined {
  font-variation-settings:
  'FILL' 1,
  'wght' 700,
  'GRAD' 200,
  'opsz' 20
}
</style>

