<template>
    <div class="task-form">
        <div class="task-form-inner">
            <form>
                <p>Name <input type="text" v-model="formObj.name"></p>
                <p>Category
                    <select v-model="formObj.category">
                        <option v-for="category in props.categories" :key="category" :value="category.toLowerCase()">
                            {{ category }}
                        </option>
                    </select>
                </p>
            </form>
            <button class="confirm-btn" @click="confirmForm">Confirm</button>
            <button class="cancel-btn" @click="close">Cancel</button>
        </div>
    </div>
    
</template>

<script setup>
import { onMounted, ref } from 'vue'
import _ from 'lodash'

const emit = defineEmits(['close', 'addTask'])
const props = defineProps({
    task: Object,
    categories: Array,
})

onMounted(() => {
    if (props.task) {
        formObj.value = _.merge(formObj.value, props.task)
        console.log(formObj.value)
    }
})
const formObj = ref({
    id: Math.floor(Math.random() * 1000),
    name: '',
    category: '',
    completed: false,
})

function close() {
    emit('close')
}
function confirmForm() {
    if (formObj.value.name && formObj.value.category) {
        emit('addTask', formObj.value)
        formObj.value = {
            name: '',
            category: '',
            completed: false,
            id: Math.floor(Math.random() * 1000),
        }
        close()
    }
}
</script>

<style scoped>
p {
    font-family: 'Poppins', sans-serif;
    font-size: 16px;
    margin-bottom: 10px;
}
select, input {
    width: auto;
    padding: 5px;
    margin: 10px 0;
    border-radius: 5px;
    border: 1px solid #ccc;
}
.task-form {
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    z-index: 99;
    background-color: rgba(0, 0, 0, 0.2);
    
    display: flex;
    align-items: center;
    justify-content: center;

}
.task-form-inner {
    /* border: 10px solid; */
    border-radius: 7px;
    background: #fff;
    padding: 32px;

}
.confirm-btn {
    border: 1px solid #635BFF;
    border-radius: 7px;
    font-family: 'Poppins', sans-serif;
    background-color: #635BFF;
    color: white;
    padding: 10px 25px;
    float: right;
    margin-top: 20px;

}
.cancel-btn {
    border: 1px solid rgb(224, 151, 151);
    font-family: 'Poppins', sans-serif;
    border-radius: 7px;
    background-color: rgb(224, 151, 151);
    color: white;
    padding: 10px 10px;
    float: right;
    margin-top: 20px;
    margin-right: 5px;
}
</style>