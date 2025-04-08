<template>
  <button 
    class="action-button" 
    :title="title" 
    @click="$emit('click')"
    :style="{ 
      backgroundColor: color,
      '--hover-color': hoverColor 
    }"
  >
    <svg 
      xmlns="http://www.w3.org/2000/svg" 
      viewBox="0 0 24 24" 
      fill="none" 
      stroke="currentColor" 
      stroke-width="2" 
      stroke-linecap="round" 
      stroke-linejoin="round"
      class="button-icon"
    >
      <template v-if="icon === 'edit'">
        <path d="M17 3a2.828 2.828 0 1 1 4 4L7.5 20.5 2 22l1.5-5.5L17 3z"></path>
      </template>
      
      <template v-else-if="icon === 'delete'">
        <polyline points="3 6 5 6 21 6"></polyline>
        <path d="M19 6v14a2 2 0 0 1-2 2H7a2 2 0 0 1-2-2V6m3 0V4a2 2 0 0 1 2-2h4a2 2 0 0 1 2 2v2"></path>
      </template>
      
      <template v-else-if="icon === 'add'">
        <line x1="12" y1="5" x2="12" y2="19"></line>
        <line x1="5" y1="12" x2="19" y2="12"></line>
      </template>
      
      <template v-else-if="icon === 'check'">
        <polyline points="20 6 9 17 4 12"></polyline>
      </template>
    </svg>
  </button>
</template>

<script setup>
const props = defineProps({
  icon: {
    type: String,
    required: true,
    validator: (value) => ['edit', 'delete', 'add', 'check'].includes(value)
  },
  color: {
    type: String,
    default: '#3498db'
  },
  hoverColor: {
    type: String,
    default: '#2980b9'
  },
  title: {
    type: String,
    default: 'Action'
  }
});

defineEmits(['click']);
</script>

<style scoped>
.action-button {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 40px;
  height: 40px;
  border-radius: 50%;
  border: none;
  color: white;
  cursor: pointer;
  transition: background-color 0.2s;
}

.action-button:hover {
  background-color: var(--hover-color);
}

.button-icon {
  width: 18px;
  height: 18px;
}
</style>