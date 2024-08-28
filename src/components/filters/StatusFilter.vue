<template>
  <select v-model="selectedStatus" @change="filterByStatus" class="custom-dropdown">
      <option selected value="all">All</option>
      <option v-for="status in props.status" :key="status" :value="status.toLowerCase()">
          {{ status }}
      </option>
  </select>
</template>

<script setup>

import { ref } from 'vue'
const emit = defineEmits(['filterByStatus'])
const props = defineProps({
    status: Array,
})
const selectedStatus = ref('')

function filterByStatus() {
  // console.log(selectedStatus.value)
    emit('filterByStatus', selectedStatus.value.toLowerCase())
}

</script>

<style scoped>

select {
  display: flex;
  margin: 10px;
  background-color: #635BFF; /* match the background color */
  color: white; /* text color */
  border: none;
  border-radius: 5px; /* rounded corners */
  padding: 5px 10px;
  font-size: 14px;
  text-align: left;
  cursor: pointer;
  font-weight: bold;
}

select option {
  color: white ; /* options text color */
  font-weight: bold;
  font-size: 14px;
}


</style>
