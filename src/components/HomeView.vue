<script setup>
import TaskInput from './TaskInput.vue'
import FilterInput from './FilterInput.vue'
import TaskView from './TaskView.vue'


import { ref } from 'vue'
const tasks = ref([
  { id: 1, text: 'Learn Vue 3', completed: false },
  { id: 2, text: 'Build a todo app', completed: false },
  { id: 3, text: 'Master component composition', completed: false }
]);

const updateTaskStatus = (taskData) => {
  const taskIndex = tasks.value.findIndex(task => task.id === taskData.id);
  if (taskIndex !== -1) {
    tasks.value[taskIndex].completed = taskData.completed;
  }
};

const editTask = (taskId) => {
  // Implement editing logic
  console.log(`Editing task ${taskId}`);
};

const deleteTask = (taskId) => {
  tasks.value = tasks.value.filter(task => task.id !== taskId);
};

// const showAddTaskForm = () => {
//   // Implement add task logic
//   console.log("Opening add task form");
// };
const handleAddTodo = (todo) => {
  // Handle the new todo here
  console.log('New todo:', todo)
  // Add it to your todos array or perform other actions
}
</script>

<template>
  <div class="app">
    <TaskInput @add-todo="handleAddTodo" />
    <FilterInput />
    <TaskView
      v-for="task in tasks"
      :key="task.id"
      :id="task.id"
      :text="task.text"
      :completed="task.completed"
      @complete="updateTaskStatus"
      @edit="editTask(task.id)"
      @delete="deleteTask(task.id)"
    />
  </div>
</template>

<style></style>
