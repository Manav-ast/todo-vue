<template>
  <div class="filter-container">
    <div class="filter-header" @click="toggleDropdown">
      <span>Filter</span>
      <span class="selected-filter">{{ selectedFilter }}</span>
      <span class="dropdown-arrow" :class="{ 'arrow-up': isOpen }">▼</span>
    </div>

    <div v-if="isOpen" class="dropdown-content">
      <div
        v-for="option in filterOptions"
        :key="option"
        class="filter-option"
        :class="{ selected: selectedFilter === option }"
        @click="selectFilter(option)"
      >
        {{ option }}
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

// Props with default values
const props = defineProps({
  initialFilter: {
    type: String,
    default: 'All',
  },
  options: {
    type: Array,
    default: () => ['All', 'Completed', 'Remaining'],
  },
})

// Reactive state
const isOpen = ref(false)
const selectedFilter = ref(props.initialFilter)
const filterOptions = ref(props.options)

// Emit events when filter changes
const emit = defineEmits(['filter-changed'])

// Methods
const toggleDropdown = () => {
  isOpen.value = !isOpen.value
}

const selectFilter = (option) => {
  selectedFilter.value = option
  isOpen.value = false
  emit('filter-changed', option)
}
</script>

<style scoped>
.filter-container {
  margin-top: 10px;
  position: relative;
  width: 100%;
  /* font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif; */
}

.filter-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 12px 16px;
  background-color: white;
  border-radius: 8px 8px 0 0;
  cursor: pointer;
  border-bottom: 1px solid #ddd;
  user-select: none;
  color: #555;
}

.dropdown-arrow {
  font-size: 12px;
  transition: transform 0.2s ease;
}

.arrow-up {
  transform: rotate(180deg);
}

.dropdown-content {
  position: absolute;
  width: 100%;
  background-color: white;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  z-index: 10;
  border-radius: 0 0 4px 4px;
  overflow: hidden;
  color: #555;
}

.filter-option {
  padding: 12px 16px;
  cursor: pointer;
  transition: background-color 0.2s;
}

.filter-option:hover {
  background-color: #f9f9f9;
}

.filter-option.selected {
  background-color: #f3f3f3;
  font-weight: 500;
}
</style>
