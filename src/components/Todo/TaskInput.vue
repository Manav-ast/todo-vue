<template>
  <div class="todo-input-container">
    <div class="todo-input-wrapper">
      <input 
        type="text" 
        v-model="todoText" 
        placeholder="Enter Todo here" 
        class="todo-input"
        @keyup.enter="addTodo"
      />
      <button class="add-button" @click="addTodo">
        <span class="plus-icon">+</span>
      </button>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const todoText = ref('');
const emit = defineEmits(['add-todo']);

const addTodo = () => {
  if (todoText.value.trim()) {
    emit('add-todo', todoText.value);
    todoText.value = '';
  }
};
</script>

<style>
.todo-input-container {
  background-color: #fff;
  border-radius: 8px;
  padding: 20px;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.05);
  width: 100%;
  max-width: 1200px; /* Increased from 800px to 1200px */
  margin: 0 auto;
}

.todo-input-wrapper {
  display: flex;
  align-items: center;
  position: relative;
  width: 100%;
}

.todo-input {
  flex-grow: 1;
  border: none;
  border-bottom: 1px solid #e0e0e0;
  padding: 12px 0;
  font-size: 16px;
  color: #555;
  background-color: transparent;
  outline: none;
  width: calc(100% - 40px);
  /* Add more horizontal space */
  min-height: 24px;
  margin-bottom: 12px; /* Extra space at bottom */
}

.todo-input::placeholder {
  color: #999;
  font-weight: 400;
}

.add-button {
  position: absolute;
  right: 0;
  top: 50%;
  transform: translateY(-60%); /* Adjusted to account for increased input height */
  width: 32px;
  height: 32px;
  border-radius: 50%;
  background-color: #6c6c6c;
  color: white;
  border: none;
  display: flex;
  justify-content: center;
  align-items: center;
  cursor: pointer;
  transition: background-color 0.2s;
}

.add-button:hover {
  background-color: #555;
}

.plus-icon {
  font-size: 20px;
  font-weight: bold;
}

/* Media query for even wider screens */
@media (min-width: 1400px) {
  .todo-input-container {
    max-width: 1400px;
  }
}
</style>