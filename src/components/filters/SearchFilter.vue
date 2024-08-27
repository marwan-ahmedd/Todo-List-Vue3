<template>
    <input type="text" v-model="searchContent" @input="filterBySearch" />
</template>


<script setup>
import { ref } from 'vue'
const searchContent = ref('')
const emit = defineEmits(['filterBySearch'])

function filterBySearch() {
    emit('filterBySearch', searchContent.value)
}
</script>

<style scoped>
input {
    width: 50%;
    padding: 5px;
    margin: 10px 0;
    border-radius: 5px;
    border: 1px solid #ccc;
}
</style>