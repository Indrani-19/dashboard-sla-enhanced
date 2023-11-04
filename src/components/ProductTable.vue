<template>
    <table>
      <thead>
        <tr class="dashboard-sla-header">
          <td :colspan="columns.length">Dashboard SLA</td>
        </tr>
        <tr class="ww-product-info-header">
          <th colspan="3">{{ wwData }}</th>
          <th colspan="9">Product Info</th>
        </tr>
        <tr>
          <th v-for="column in columns" :key="column.name">{{ column.name }}</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="row in rawData" :key="row.id" :class="statusClass(row.Status)">
          <td v-for="column in columns" :key="column.value">{{ row[column.value] }}</td>
        </tr>
      </tbody>
    </table>
  </template>
  
  <script>
  function getWWFromDate(date = new Date()) {
    let currentDate = date;
    let startDate = new Date(currentDate.getFullYear(), 0, 1);
    let days = Math.floor((currentDate - startDate) / (24 * 60 * 60 * 1000));
    
    return {
      year: currentDate.getFullYear(),
      workweek: Math.ceil(days / 7),
      numofday: currentDate.getDay(),
    };
  }
  
  export default {
    props: {
      rawData: Array
    },
    computed: {
      wwData() {
        const wwInfo = getWWFromDate();
        return `${wwInfo.year}WW${wwInfo.workweek}.${wwInfo.numofday}`;
      }
    },
    data() {
      return {
        columns: [
          { name: "Status", value: "Status" },
          { name: "Cores", value: "Cores" },
          { name: "Product", value: "Product" },
          { name: "Lithography", value: "Lithography" },
          { name: "Threads", value: "Threads" },
          { name: "Base Freq", value: "Base_Freq" },
          { name: "Max Turbo Freq", value: "Max_Turbo_Freq" },
          // Add other columns as needed
        ]
      };
    },
    methods: {
      statusClass(status) {
        return `status-${status.replace(/\s+/g, '').replace(/[\(\)]/g, '').toLowerCase()}`;
      },
    }
  };
  </script>
  
  <style scoped>
  table {
    border-collapse: collapse;
    width: 100%;
    border: 1px solid #ddd;
    font-size: 18px;
  }
  
  table th, table td {
    text-align: left;
    padding: 12px;
    border-left: 1px solid #ddd; /* Add vertical lines for columns */
  }
  
  table th:first-child, table td:first-child {
    border-left: none; /* Remove border from the first cell */
  }
  
  table tr {
    border-bottom: 1px solid #ddd;
  }
  
  .dashboard-sla-header td {
    background-color:  #337AB7; /* Green background */
    color: white; /* White text color */
    font-weight: bold;
    text-align: center; /* Center align text */
    vertical-align: middle; /* Center vertically */
  }
  
  .ww-product-info-header th {
    background-color: #337AB7; /* Blue background for WW data header */
    color: white;
    text-align: center;
    font-weight: bold;
  }
  
  /* CSS classes for statuses */
  .status-announced {
    background-color: rgb(167, 89, 89);
  }
  
  .status-launched {
    background-color: rgb(120, 54, 156);
  }
  
  .status-discontinued {
    background-color: rgb(168, 184, 44);
  }
  
  .status-launchedwithipu {
    background-color: rgb(172, 78, 170);
  }

  
  /* Add additional status classes if needed */
  </style>
  