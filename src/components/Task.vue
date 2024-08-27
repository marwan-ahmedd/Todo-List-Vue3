<template>
    <div class="task" @mouseover="isHovered = true" @mouseleave="isHovered = false">
        <input type="checkbox" v-model="task.completed" />
        <strike v-if="task.completed"> {{ task.name }}</strike>
        <span v-else>{{ task.name }}</span>
        <!-- {{ task.date }} -->
        <div v-if="isHovered" class="actions">
            <button @click="editTask"><i class="fas fa-edit"></i></button>
            <button @click="deleteTask"><i class="fas fa-trash-alt"></i></button>
        </div>
    </div>
</template>

<script setup>
import { ref } from 'vue'
const emit = defineEmits(['editTask', 'deleteTask'])

const isHovered = ref(false)
const props = defineProps({
    task: Object,
})
function editTask() {
    emit('editTask', props.task)
    // console.log('edit', props.task)
}
function deleteTask() {
    emit('deleteTask', props.task.id)
}
</script>

<style scoped>
.task {
    display: flex;
    align-items: left;
    padding: 10px;
    border: 1px solid #ccc;
    border-radius: 5px;
    margin-bottom: 10px;
    justify-content: space-between;
}

.task strike {
    flex-grow: 1;
    text-align: left;
}
.task span {
    flex-grow: 1;
    text-align: left;
}
.actions {
    display: flex;
    gap: 10px;
}
input {
    margin-right: 7px;
}
button i {
    color: #635BFF;
}
</style>