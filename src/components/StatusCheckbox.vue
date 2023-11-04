<template>
    <label :for="`status-${status}`" class="status-checkbox">
      <input
        :id="`status-${status}`"
        type="checkbox"
        :value="status"
        @change="toggle"
      />
      {{ status }}
    </label>
  </template>
  
  <script>
  export default {
    props: ['status'],
    methods: {
      toggle(event) {
        this.$emit('toggle', {
            name: this.status,
            checked: event.target.checked
        });
      }
    }
  };
  </script>
  
  <style scoped>
  .status-checkbox {
    display: inline-block;
    margin-right: 10px;
  }
  
  .status-checkbox input[type="checkbox"] {
    margin-right: 5px;
  }
  </style>
  