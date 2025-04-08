<script setup>
import TaskInput from '../Todo/TaskInput.vue'
import FilterInput from '../Todo/FilterInput.vue'
import TaskView from '../Todo/TaskView.vue'
import EditModal from '../Todo/EditTask.vue'

import { ref, computed } from 'vue'
const tasks = ref([
  { id: 1, text: 'Learn Vue 3', completed: false },
  { id: 2, text: 'Build a todo app', completed: false },
  { id: 3, text: 'Master component composition', completed: false },
])

// For filtering
const currentFilter = ref('All');

// Computed property to filter tasks based on the selected filter
const filteredTasks = computed(() => {
  switch (currentFilter.value) {
    case 'Completed':
      return tasks.value.filter(task => task.completed);
    case 'Remaining':
      return tasks.value.filter(task => !task.completed);
    default:
      return tasks.value;
  }
});

const changeFilter = (filter) => {
  currentFilter.value = filter;
};

const isEditModalOpen = ref(false)
const editingTask = ref({ id: null, text: '' })

const openEditModal = (task) => {
  editingTask.value = task
  isEditModalOpen.value = true
}

const closeEditModal = () => {
  isEditModalOpen.value = false
  editingTask.value = { id: null, text: '' }
}

const saveEditedTask = (taskData) => {
  const taskIndex = tasks.value.findIndex(task => task.id === taskData.id);
  if (taskIndex !== -1) {
    tasks.value[taskIndex].text = taskData.text;
  }
};

const updateTaskStatus = (taskData) => {
  const taskIndex = tasks.value.findIndex((task) => task.id === taskData.id)
  if (taskIndex !== -1) {
    tasks.value[taskIndex].completed = taskData.completed
  }
}

const deleteTask = (taskId) => {
  tasks.value = tasks.value.filter((task) => task.id !== taskId)
}

// const showAddTaskForm = () => {
//   // Implement add task logic
//   console.log("Opening add task form");
// };
const handleAddTodo = (todo) => {
  // Handle the new todo here

  tasks.value.push({
    id: tasks.value.length + 1,
    text: todo,
    completed: false,
  })
  // console.log('New todo:', todo)
  // Add it to your todos array or perform other actions
}
</script>

<template>
  <div class="app">
    <TaskInput @add-todo="handleAddTodo" />
    <!-- Filter Component -->
    <FilterInput 
      :initialFilter="currentFilter" 
      @filter-changed="changeFilter" 
    />
    <div class="tasks-container">
      <!-- Only show filtered tasks -->
      <TaskView
        v-for="task in filteredTasks"
        :key="task.id"
        :id="task.id"
        :text="task.text"
        :completed="task.completed"
        @complete="updateTaskStatus"
        @edit="openEditModal(task)"
        @delete="deleteTask(task.id)"
      />
      
      <div v-if="filteredTasks.length === 0" class="empty-state">
        <p v-if="tasks.length === 0">No tasks yet. Add one to get started!</p>
        <p v-else>No {{ currentFilter.toLowerCase() }} tasks found.</p>
      </div>
    </div>
    <!-- Edit Task Modal -->
    <EditModal
      :is-open="isEditModalOpen"
      :task-text="editingTask.text"
      :task-id="editingTask.id"
      @close="closeEditModal"
      @save="saveEditedTask"
    />
  </div>
</template>

<style>
.tasks-container {
  margin: 20px 0;
  height: 50vh;
  overflow-y: scroll;
}

.empty-state {
  text-align: center;
  margin-top: 20px;
  font-size: 18px;
  color: #999;
}
</style>
