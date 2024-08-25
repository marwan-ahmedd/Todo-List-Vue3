<template>
    <div class="container">
        <SearchFilter @filterBySearch="filterBySearch" />
        <StatusFilter class="category-filter" :status="props.status" @filterByStatus="filterByStatus" />
    </div>
</template>

<script setup>
import { ref } from 'vue'
import StatusFilter from './StatusFilter.vue';
import SearchFilter from './SearchFilter.vue';

const props = defineProps({
    status: Array,
})

const emit = defineEmits(['filterBySearch', 'filterByStatus', 'filterByCategory'])

function filterBySearch(search) {
    emit('filterBySearch', search)
}
function filterByStatus(status) {
    emit('filterByStatus', status)
}
function filterByCategory(filters) {
    emit('filterByCategory', filters)
}
</script>

<style scoped>

.container {
    width: 100%;
    padding: 10px;
    display: flex;
    align-items: center;
}
</style>