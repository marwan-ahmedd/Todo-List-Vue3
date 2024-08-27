<template>
  <div class="container">
      <FilterTasks :status="status" @filterBySearch="filterBySearch" @filterByStatus="filterByStatus" @filterByCategory="filterByCategory" />
      <Tasks :filteredValues="filterValues" /> 
     <button class="add-task" @click="toggleTaskForm"><i class="fas fa-plus"></i></button>
     <TaskForm v-show="showTaskForm" />
  </div>
</template>

<script setup>
import Tasks from './components/Tasks.vue'
import FilterTasks from './components/filters/FilterTasks.vue'
import TaskForm from './components/TaskForm.vue'

import { ref } from 'vue'

const filterValues = ref({})
const showTaskForm = ref(false);
const status = ref(['Completed', 'Uncompleted'])

function filterBySearch(filteredSearch) {
  filterValues.value = { ...filterValues.value, search: filteredSearch }
}
function filterByStatus(filteredStatus) {
  filterValues.value = { ...filterValues.value, status: filteredStatus }
}
function filterByCategory(filteredCategory) {
  filterValues.value = { ...filterValues.value, category: filteredCategory }
}

function toggleTaskForm() {
  showTaskForm.value = !showTaskForm.value
  // console.log(showTaskForm.value)
}
</script>

<style>
#app {
  padding: 60px 0;
}
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
button {
  cursor: pointer;
  font: 13px/1.4 "Poppins", sans-serif;
  color: red;
  background-color: white;
  border: none;
  transition: all 0.3s linear;
}
body {
  font: 15px/1.4 'Poppins', sans-serif;
  background: #fff;
  color: #333
}
.container {
  max-width: 480px;
  margin: 0 auto;
  padding: 0 15px;
}
.add-task {
  float: right;
  color: white;
  background-color: #635BFF;
  border: 7px solid #635BFF;
  border-radius: 50%;
  padding: 4px;
  display: flex;
  align-items: center;
  justify-content: center;
  
}
</style>
