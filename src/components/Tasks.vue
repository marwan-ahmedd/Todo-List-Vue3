<template>
    <div class="tasksList">
        <div :key="task.id" v-for="task in filteredTasks">
            <Task :task="task" @deleteTask="deleteTask" />
        </div>
    </div>
</template>

<script setup>
import { ref, watch } from 'vue'
import Task from './Task.vue'

const props = defineProps({
    filteredValues: Object
})


const tasksList = ref([
  {
    id: 1, 
    name: 'Vacation Planning',
    completed: false,
    date: '',
    category: ''
  },
  {
    id: 2,
    name: 'Cook Dinner',
    completed: false,
    date: '',
    category: ''
  },
  {
    id: 3,
    name: 'Finish Math Assignment',
    completed: false,
    date: '',
    category: ''
  },
  {
    id: 4,
    name: 'Read a book',
    completed: false,
    date: '',
    category: ''
  }
])

const filteredTasks = ref(Array.from(tasksList.value));

function filterSearch() {
    const searchValues = props?.filteredValues?.search;
    filteredTasks.value = tasksList?.value?.filter((task) => 
        task.name?.toLowerCase().includes(searchValues.toLowerCase())
    )
}
function filterStatus() {
  const statusValues = props?.filteredValues?.status;
  statusValues = statusValues.toLowerCase()
  filteredValues.value = tasksList?.value?.filter((task) => 
      statusValues == 'all' || (task.completed == true && statusValues == 'completed') || (task.completed == false && statusValues == 'uncompleted')
  )
}
// console.log(props.filteredValues);
watch(() => Object.values(props?.filteredValues), () => {
    filterSearch()
    // filterStatus()
})

function deleteTask(id) {
  console.log('delete', id)
  filteredTasks.value = filteredTasks.value.filter((task) => task.id !== id)
}
</script>


<style scoped>
.tasksList li {
  display: flex;
  justify-content: space-between;
}

</style>