<template>
    <div class="tasksList">
        <div :key="task.id" v-for="task in props.tasks">
            <Task :task="task" @deleteTask="deleteTask" @editTask="editTask" />
        </div>
    </div>
</template>

<script setup>
import { ref, watch } from 'vue'
import Task from './Task.vue'

const emit = defineEmits(['editTask'])
const props = defineProps({
    tasks: Array,
})


function filterStatus() {
  const statusValues = props?.filteredValues?.status;
  statusValues = statusValues.toLowerCase()
  filteredValues.value = props.tasks?.filter((task) => 
      statusValues == 'all' || (task.completed == true && statusValues == 'completed') || (task.completed == false && statusValues == 'uncompleted')
  )
}

function deleteTask(id) {
  emit('deleteTask', id)
}
function editTask(task) {
  emit('editTask', task)
}
</script>


<style scoped>
.tasksList li {
  display: flex;
  justify-content: space-between;
}

</style>