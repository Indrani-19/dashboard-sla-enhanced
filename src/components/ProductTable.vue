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
        <th v-for="column in columns.filter((col) => !col.hidden)" :key="column.name">{{ column.name }}</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="row in rows" :key="row.id" :class="statusClass(row.Status)">
        <td v-if="!!row.rowspan" :rowspan="row.rowspan">{{ row['Status'] }}</td>
        <td v-for="column in columns.filter((col) => col.value !== 'Status' && !col.hidden)" :key="column.value">{{ row[column.value] }}</td>
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
    rows: function() {
      const counts = [];
      for (const row of this.rawData) {
        if (!!counts.length && counts[counts.length - 1].Status === row.Status) {
          counts[counts.length - 1].count++;
        } else {
          counts.push({ Status: row.Status, count: 1 });
        }
      }
      console.log(counts);
      const rows = [];
      let rowspanAdded = false;
      for (const data of this.rawData) {
        const row = { ...data };
        if (!rowspanAdded) {
          row.rowspan = counts[0].count;
          rowspanAdded = true;
        }
        counts[0].count--;
        if (!counts[0].count) {
          counts.shift();
          rowspanAdded = false;
        }
        rows.push(row);
      }
      console.log(rows, counts);
      return rows;
    }
  },
  data() {
    return {
      columns: [
        { name: "Temp", value: "rowspan", hidden: true },
        { name: "Status", value: "Status"},
        { name: "Cores", value: "Cores" },
        { name: "Product", value: "Product" },
        { name: "Lithography", value: "Lithography" },
        { name: "Threads", value: "Threads" },
        { name: "Base Freq", value: "Base_Freq" },
        { name: "Max Turbo Freq", value: "Max_Turbo_Freq" },
      ]
    };
  },
  methods: {
    statusClass(status) {
      return `status-${status.replace(/\s+/g, '').replace(/[\(\)]/g, '').toLowerCase()}`;
    },
    populateRowSpan(rawData= []) {
      
    }
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
    border-left: 1px solid #ddd;
     
  }
   
  table tr {
    border-bottom: 1px solid #ddd;
  }
  
  .dashboard-sla-header td {
    background-color:  #337AB7; 
    color: white;
    font-weight: bold;
    text-align: center; 
    vertical-align: middle; 
  }
  
  .ww-product-info-header th {
    background-color: #337AB7; 
    color: white;
    text-align: center;
    font-weight: bold;
  }
  
  /* CSS classes for statuses */
  .status-announced {
    background-color: rgb(147, 94, 50);
  }
  
  .status-launched {
    background-color: rgb(172, 78, 170);
  }
  
  .status-discontinued {
    background-color: rgb(61, 160, 182);
  }
  
  .status-launchedwithipu {
    background-color: rgb(84, 223, 84);
  }

  
  </style>
  