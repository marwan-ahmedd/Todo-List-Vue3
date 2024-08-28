<template>
    <div class="task">
        <div class="task-details" >
            <input type="checkbox" v-model="task.completed" />
            <span class="strick" v-if="task.completed"> {{ task.name }}</span>
            <span v-else>{{ task.name }}</span>
            
        </div>
        <div class="actions">
            <button @click="editTask"><i class="fas fa-edit"></i></button>
            <button @click="deleteTask"><i class="fas fa-trash-alt"></i></button>
        </div>
        <span class="category">{{ props.task.category }}</span>
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
}
function deleteTask() {
    emit('deleteTask', props.task.id)
}
</script>

<style lang="scss" scoped>
.task {
    display: flex;
    padding: 10px;
    border: 1px solid #ccc;
    border-radius: 5px;
    margin-bottom: 10px;
    justify-content: space-between;
}

.task:hover {
    .actions {
        display: inline-block;
    }
}
.task-details {
    /* align-items: center; */
    /* align-content: center; */
    /* display: flex; */
}
.category {
    width:fit-content;
    border: 1px solid #635BFF;
    border-radius: 20px;
    background-color: #635BFF;
    color: white;
    padding: 3px 10px;
    margin-left: 10px;
}
.actions {
    display: none;
    width: 50px;

    gap: 10px;
}
.strick{
    text-decoration: line-through;
}
input {
    margin-right: 7px;
}
button i {
    color: #635BFF;
}
</style>