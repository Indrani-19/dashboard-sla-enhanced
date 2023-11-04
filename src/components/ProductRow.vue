<template>
    <tr>
      <td>{{ product.Product }}</td>
      <td>{{ product.Lithography }}</td>
      <td>{{ product.Threads }}</td>
      <td>{{ product.Base_Freq }}</td>
      <td>{{ product.Max_Turbo_Freq }}</td>
    </tr>
  </template>
  
  <script>
  export default {
    props: {
      product: Object
    }
  };
  </script>
</script>

<style scoped>
.product-row:nth-child(even) {
  background-color: #f9f9f9;
}

</style>  