<template>
  <div class="container">
      <FilterTasks 
        :status="status" 
        @filterBySearch="filterBySearch" 
        @filterByStatus="filterByStatus" 
        @filterByCategory="filterByCategory" />

      <Tasks 
        :tasks="tasks"  
        @editTask="editTask"
        @deleteTask="deleteTask" /> 
     <button class="add-task" @click="showTaskForm = true"><i class="fas fa-plus"></i></button>

     <TaskForm 
      v-if="showTaskForm"
      :task="selectedTask"
      :categories="categories"
      @close="close"
      @addTask="addTask" />
  </div>
</template>

<script setup>
import { ref, watch } from 'vue'
import Tasks from './components/Tasks.vue'
import FilterTasks from './components/filters/FilterTasks.vue'
import TaskForm from './components/TaskForm.vue'


const filterValues = ref({})
const showTaskForm = ref(false);
const status = ref(['Completed', 'Uncompleted'])
const categories = ref(['Work', 'Personal', 'Others'])
const selectedTask = ref(null)
const tasks = ref([
  {
    id: 1, 
    name: 'Vacation Planning',
    completed: false,
    date: '',
    category: 'Work'
  },
  {
    id: 2,
    name: 'Cook Dinner',
    completed: false,
    date: '',
    category: 'Personal'
  },
  {
    id: 3,
    name: 'Finish Math Assignment',
    completed: false,
    date: '',
    category: 'Work'
  },
  {
    id: 4,
    name: 'Read a book',
    completed: false,
    date: '',
    category: 'Others'
  }
])  

function filterBySearch(searchValues) {
    tasks.value = tasks.value.filter((task) => 
        task.name?.toLowerCase().includes(searchValues?.toLowerCase())
    )
}
function filterByStatus(filteredStatus) {
  filterValues.value = { ...filterValues.value, status: filteredStatus }
}
function filterByCategory(filteredCategory) {
  filterValues.value = { ...filterValues.value, category: filteredCategory }
}
function addTask(task) {
  console.log("pushing now", task)
  tasks.value.push(task)
  console.log(tasks.value)
}
function editTask(task) {
  selectedTask.value = task
  showTaskForm.value = true;``
}
function deleteTask(id) {
  tasks.value = tasks.value.filter(task => task.id !== id)
}
function close() {
  showTaskForm.value = !showTaskForm.value
  selectedTask.value = null
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
