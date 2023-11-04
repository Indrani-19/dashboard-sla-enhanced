<template>
    <div class="pagination">
      <button
        v-for="page in totalPages"
        :key="page"
        @click="changePage(page)"
        :class="{ active: page === currentPage }"
      >
        {{ page }}
      </button>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      totalItems: {
        type: Number,
        required: true
      },
      pageSize: {
        type: Number,
        required: true
      }
    },
    data() {
      return {
        currentPage: 1
      };
    },
    computed: {
      totalPages() {
        return Math.ceil(this.totalItems / this.pageSize);
      }
    },
    methods: {
      changePage(page) {
        this.currentPage = page;
        this.$emit('page-changed', page);
      }
    }
  };
  </script>
  
  <style>
.pagination {
    display: flex;
    justify-content: center;
    margin-top: 20px;
  }
  
  .pagination button {
    margin: 0 5px;
    padding: 5px 10px;
    border: 1px solid #ccc;
    cursor: pointer;
  }
  
  .pagination button.active {
    background-color: #007BFF;
    color: #fff;
  }  
</style>
 