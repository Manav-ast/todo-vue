<template>
  <div v-if="isOpen" class="modal-overlay" @click.self="closeModal">
    <div class="modal-container">
      <div class="modal-header">
        <h2>Edit Task</h2>
        <button class="close-button" @click="closeModal">×</button>
      </div>
      <div class="modal-body">
        <form @submit.prevent="saveTask">
          <div class="form-group">
            <label for="taskText">Task</label>
            <input 
              type="text" 
              id="taskText" 
              v-model="editedTaskText" 
              class="form-input"
              placeholder="Enter task description"
              ref="taskInput"
              autofocus
            />
          </div>
          <div class="form-actions">
            <button type="button" class="cancel-button" @click="closeModal">Cancel</button>
            <button type="submit" class="save-button">Save Changes</button>
          </div>
        </form>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, watch, nextTick } from 'vue';

const props = defineProps({
  isOpen: {
    type: Boolean,
    default: false
  },
  taskText: {
    type: String,
    default: ''
  },
  taskId: {
    type: [Number, String],
    default: null
  }
});

const emit = defineEmits(['close', 'save']);

const editedTaskText = ref(props.taskText);
const taskInput = ref(null);

// Update local text when props change
watch(() => props.taskText, (newValue) => {
  editedTaskText.value = newValue;
});

// Focus input when modal opens
watch(() => props.isOpen, async (isOpen) => {
  if (isOpen) {
    await nextTick();
    taskInput.value?.focus();
  }
});

const closeModal = () => {
  emit('close');
};

const saveTask = () => {
  if (editedTaskText.value.trim()) {
    emit('save', {
      id: props.taskId,
      text: editedTaskText.value.trim()
    });
    closeModal();
  }
};
</script>

<style scoped>
.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: rgba(0, 0, 0, 0.5);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 1000;
}

.modal-container {
  background-color: white;
  border-radius: 8px;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.2);
  width: 90%;
  max-width: 500px;
  max-height: 90vh;
  overflow-y: auto;
  animation: modal-fade 0.2s ease-out;
}

.modal-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 16px 20px;
  border-bottom: 1px solid #eee;
}

.modal-header h2 {
  margin: 0;
  font-size: 18px;
  color: #333;
}

.close-button {
  background: none;
  border: none;
  font-size: 24px;
  color: #666;
  cursor: pointer;
  padding: 0;
  margin: 0;
  line-height: 1;
}

.modal-body {
  padding: 20px;
}

.form-group {
  margin-bottom: 20px;
}

.form-group label {
  display: block;
  margin-bottom: 6px;
  font-weight: 500;
  color: #555;
}

.form-input {
  width: 100%;
  padding: 10px 12px;
  border: 1px solid #ddd;
  border-radius: 4px;
  font-size: 16px;
  transition: border-color 0.2s;
}

.form-input:focus {
  border-color: #3498db;
  outline: none;
}

.form-actions {
  display: flex;
  justify-content: flex-end;
  gap: 10px;
}

.cancel-button, .save-button {
  padding: 10px 16px;
  border-radius: 4px;
  font-size: 14px;
  cursor: pointer;
  transition: background-color 0.2s;
}

.cancel-button {
  background-color: #f1f1f1;
  border: none;
  color: #333;
}

.cancel-button:hover {
  background-color: #e1e1e1;
}

.save-button {
  background-color: #3498db;
  border: none;
  color: white;
}

.save-button:hover {
  background-color: #2980b9;
}

@keyframes modal-fade {
  from {
    opacity: 0;
    transform: translateY(-20px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}
</style>