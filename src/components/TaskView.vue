<template>
  <div class="task-container">
    <div class="task-content">
      <input
        type="checkbox"
        :checked="isCompleted"
        @change="toggleComplete"
        class="task-checkbox"
      />
      <span class="task-text" :class="{ 'completed': isCompleted }">{{ text }}</span>
    </div>
    <div class="task-actions">
      <ActionButton 
        icon="edit" 
        color="#f8a845" 
        hoverColor="#e69735" 
        title="Edit task" 
        @click="$emit('edit')" 
      />
      <ActionButton 
        icon="delete" 
        color="#e74c3c" 
        hoverColor="#c0392b" 
        title="Delete task" 
        @click="$emit('delete')" 
      />
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import ActionButton from './ActionButton.vue';

const props = defineProps({
  text: {
    type: String,
    required: true
  },
  completed: {
    type: Boolean,
    default: false
  },
  id: {
    type: [Number, String],
    required: true
  }
});

const isCompleted = ref(props.completed);

const emit = defineEmits(['complete', 'edit', 'delete']);

const toggleComplete = () => {
  isCompleted.value = !isCompleted.value;
  emit('complete', {
    id: props.id,
    completed: isCompleted.value
  });
};
</script>

<style scoped>
.task-container {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 12px 16px;
  background-color: white;
  border-radius: 6px;
  box-shadow: 0 1px 3px rgba(0, 0, 0, 0.1);
  margin-bottom: 10px;
  margin-top: 10px;
  overflow: auto;
  /* cursor: pointer; */
}

.task-content {
  display: flex;
  align-items: center;
  flex: 1;
  color: #555;
}

.task-checkbox {
  margin-right: 12px;
  width: 18px;
  height: 18px;
  cursor: pointer;
}

.task-text {
  font-size: 16px;
  word-break: break-word;
}

.task-text.completed {
  text-decoration: line-through;
  color: #888;
}

.task-actions {
  display: flex;
  gap: 8px;
}
</style>