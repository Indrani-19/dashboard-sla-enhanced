<template>
    <table>
      <thead>
        <tr>
          <td :colspan="12">Dashboard SLA</td>
        </tr>
        <tr>
          <th colspan="3">{{ wwData }}</th>
          <th colspan="8">Product Info</th>
        </tr>
        <tr>
          <th v-for="column of columns">{{ column.name }}</th>
        </tr>
      </thead>
      <tbody>
        <!-- <template v-for="(productsByCores, status) in productData" :key="status">
          <template v-if="!hideStatus.includes(status)">
            <tr v-for="(products, cores, index) in productsByCores" :key="cores">
              <td v-if="index === 0" :rowspan="calculateRowspan(productsByCores)">{{ status }}</td>
              <td>{{ cores }}</td>
              <td v-for="product of products" :key="product.id">{{ product.Product }}</td>
              <td>{{ product.Lithography }}</td>
              <td>{{ product.Threads }}</td>
              <td>{{ product.Base_Freq }}</td>
              <td>{{ product.Max_Turbo_Freq }}</td>
            </tr>
          </template>
        </template> -->
            <tr v-for="row of rawData">
                <td v-for="column of columns">{{ row[column.value] }}</td>
            </tr>
        </tbody>
    </table>
  </template>
  
  
  <script>
  // Standalone utility function outside of the component
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
      productData: Object,
      hideStatus: Array,
      rawData: Array
    },
    computed: {
      wwData() {
        const wwInfo = getWWFromDate(); // Using the standalone function
        return `${wwInfo.year}WW${wwInfo.workweek}.${wwInfo.numofday}`;
      }
    },
    data() {
        return {
            columns: [
                {
                    name: "Status",
                    value: "Status",
                },
                {
                    name:"Cores",
                    value:"Cores"
                },
                {
                    name:"Product",
                    value:"Product"
                },

                {
                    name:"Lithography",
                    value:"Lithography"
                },

                {
                    name:"Threads",
                    value:"Threads"
                },
                {
                    name: "Base Freq",
                    value: "Base_Freq"
                },
                {
                    name:"x Turbo Freq",
                    value:"Max_Turbo_Freq"
                }
            ]
                
        }
    },
    methods: {
      calculateRowspan(data) {
        let sum = 0;
        for (const cores in data) {
          sum += data[cores].length + 1;
        }
        return sum;
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
  }
  
  table tr {
    border-bottom: 1px solid #ddd;
  }
  
  table th {
    background-color: #f2f2f2;
    color: black;
  }
  
  .width1 {
    width: 1%;
    white-space: nowrap;
  }
  
  .innerCells {
    display: flex;
    justify-content: center;
    align-items: center;
  }
  
  .productColumn {
    background-color: white;
  }
  
  input[disabled] {
    cursor: text;
    background-color: inherit;
    color: black;
    border: none;
  }
  
  /* Additional styles if necessary */
  </style>
  