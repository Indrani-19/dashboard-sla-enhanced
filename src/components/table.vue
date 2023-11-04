<template>
  <div id="the-table">
    <StatusBar :status-list="productDataByStatus.status" @toggle="handleFilters" />
    <ProductTable :raw-data="paginatedData" />
    <Pagination
      :total-items="totalItems"
      :page-size="pageSize"
      :current-page="currentPage"
      @page-changed="changePage"
    />
  </div>
</template>

<script setup>
import { ref, computed } from 'vue';
import StatusBar from './StatusBar.vue';
import ProductTable from './ProductTable.vue';
import Pagination from './Pagination.vue'; 
import data from '../assets/data.json';

// Constants for pagination
const pageSize = 100; 
const currentPage = ref(1); 

// Other reactive references and functions
const hidestatus = ref([]);
const filters = ref(new Map());

// Function to handle filter changes
const handleFilters = ({ name, checked }) => {
  filters.value.set(name, checked);
};

// Computed property for organizing data by status
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
  };
});

// Computed property for filtering data
const getFilteredRows = computed(() => {
  const filteredData = [];
  data.forEach((row) => {
    const status = row['Status'];
    if (!filters.value.has(status) || filters.value.get(status)) {
      filteredData.push(row);
    }
  });
  return { filteredData };
});

// Computed property for paginated data
const paginatedData = computed(() => {
  const startIndex = (currentPage.value - 1) * pageSize;
  const endIndex = startIndex + pageSize;
  return getFilteredRows.value.filteredData.slice(startIndex, endIndex);
});

// Computed property to get the total number of items for pagination
const totalItems = computed(() => getFilteredRows.value.filteredData.length);

// Method to change the current page
const changePage = (page) => {
  currentPage.value = page;
};
</script>

<style scoped>
#the-table {
  padding: 20px;
  font-family: 'Arial', sans-serif;
  background-color: black;
  color: white; 
}
</style>
