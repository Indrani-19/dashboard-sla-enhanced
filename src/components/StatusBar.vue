<template>
    <div class="hideBar">
      <label class="hideLabel">Hide:</label>
      <div class="checkbox">
        <StatusCheckbox
          v-for="status in statusList"
          :key="status"
          :status="status"
          @toggle="handleToggle"
        />
      </div>
    </div>
  </template>
  
  <script>
  import StatusCheckbox from './StatusCheckbox.vue';
  
  export default {
    components: {
      StatusCheckbox
    },
    props: {
      statusList: Array
    },
    methods: {
      handleToggle(toggleEvent) {
        this.$emit('toggle', toggleEvent);
      }
    }
  };
  </script>
<style scoped>
.status-bar {
  margin-bottom: 20px;
}

.hideLabel {
  margin-right: 10px;
}

.checkbox {
  display: inline-block;
  margin-right: 5px;
}
.hideBar {
  display: flex;
  justify-content: center;
  align-items: center;
  margin-bottom: 20px;
}
</style>  