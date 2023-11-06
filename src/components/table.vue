<template>
  <div id="the-table">
    <StatusBar :status-list="getAllStatuses" @toggle="handleFilters" />
    
    <div class="search-bar">
      <input type="text" v-model="searchTerm" placeholder="Search" />
    </div>
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

const pageSize = 100;
const currentPage = ref(1);

const hidestatus = ref([]);
const filters = ref(new Map());
const searchTerm = ref(""); 

const handleFilters = ({ name, checked }) => {
  filters.value.set(name, checked);
};

const productDataByStatus = computed(() => {
  let organizedData = {};
  let statusSet = new Set(data.map(item => item.Status));

  data.forEach(element => {
    if (hidestatus.value.includes(element.Status)) return;
    if (!organizedData[element.Status]) {
      organizedData[element.Status] = {};
    }
    let cores = element.Cores;
    if (!organizedData[element.Status][cores]) {
      organizedData[element.Status][cores] = [];
    }
    organizedData[element.Status][cores].push(element);
  });

  return {
    status: Array.from(statusSet).sort(),
    data: organizedData,
  };
});

const getAllStatuses = computed(() => {
  return [
    'All Statuses',
    ...new Set(data.map(({Status}) => Status))
  ];
});

const getFilteredRows = computed(() => {
  const filteredData = data.filter((row) => {
    let statusMatch = !filters.value.has(row.Status) || !filters.value.get(row.Status);
    if (filters.value.has('All Statuses') && !!filters.value.get('All Statuses')) {
      statusMatch = false;
    }
    const searchMatch = Object.values(row).some(
      (value) => value.toString().toLowerCase().includes(searchTerm.value.toLowerCase())
    );
    return statusMatch && (searchMatch || searchTerm.value === '');
  });
  return filteredData;
});

const paginatedData = computed(() => {
  const startIndex = (currentPage.value - 1) * pageSize;
  const endIndex = startIndex + pageSize;
  return getFilteredRows.value.slice(startIndex, endIndex);
});

const totalItems = computed(() => getFilteredRows.value.length);

const changePage = (page) => {
  currentPage.value = page;
};
</script>

<style scoped>
#the-table {
  padding: 20px;
  font-family: 'Arial', sans-serif;
  background-color: #fff;
  color: #333;
}
.search-bar-container {
  margin-top: 10px; 
  text-align: center; 
}


.search-bar {
  background-color: black;
  padding: 5px 10px;
  display: flex;
  align-items: center;
  position: fixed; 
  top: 5px; 
  width: 50%; 
  z-index: 100;
  height: 2%;
  justify-content:center; 
  margin-left: 20%;
}

.search-bar::placeholder {
  font-size: 10px; 
}
</style>
