
<template>
  <div id="the-table">
    <StatusBar :status-list="productDataByStatus.status" @toggle="handleFilters" />
    <ProductTable :raw-data="getFilteredRows.filteredData" />

    
  </div>
</template>

<script setup>
import { ref, computed } from 'vue';
import StatusBar from './StatusBar.vue';
import ProductTable from './ProductTable.vue';
import data from '../assets/data.json';

const hidestatus = ref([]);
const filters = ref(new Map());

// // Function to get workweek information from a date
// function getWWFromDate(date = new Date()) {
//   const startOfYear = new Date(date.getFullYear(), 0, 1);
//   const days = Math.floor((date - startOfYear) / (24 * 60 * 60 * 1000));
//   return {
//     year: date.getFullYear(),
//     workweek: Math.ceil((startOfYear.getDay() + 1 + days) / 7),
//     numofday: date.getDay(),
//   };
// }

// Function to toggle the visibility of product status
const handleFilters = ({ name, checked }) => {
  filters.value.set(name, checked);
  console.log(filters);
};

// Computed property to get product data organized by status
const productDataByStatus = computed(() => {
  let organizedData = {};
  let statusSet = new Set(data.map(item => item.Status));

  data.forEach(element => {
    if (hidestatus.value.includes(element.Status)) return;
    if (!organizedData[element.Status]) organizedData[element.Status] = {};
    let cores = element.Cores;
    if (!organizedData[element.Status][cores]) organizedData[element.Status][cores] = [];
    organizedData[element.Status][cores].push(element);
  });

  return {
    status: Array.from(statusSet).sort(),
    data: organizedData,
  }});

  // filtering data based on the hide checkboxes
  const getFilteredRows = computed(() => {
    const filteredData = [];
    data.forEach((row) => {
      const status = row['Status'];
      if (!filters.value.has(status) || !filters.value.get(status)) {
        filteredData.push(row);
      }
    });
    return { filteredData };
  });
</script>

<style scoped>
#the-table {
  padding: 20px;
  font-family: 'Arial', sans-serif;
}
</style>


