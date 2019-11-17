<template>
  <div id="customerList">
    <table>
      <thead>
      <tr>
        <th>Name</th>
        <th>Email</th>
        <th>Juices</th>
      </tr>
      </thead>
      <tbody>
      <tr>
          <tr v-for="customer in customers" :key="customer.id">
          <td>{{ customer.name }}</td>
          <td>{{ customer.email }}</td>
          <td>
              <ul>
                  <li v-for="(juice, $index) in customer.juices" :key="$index">{{ juice }}</li>
              </ul>
          </td>
      </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
  export default {
    name: "CustomerList",
    props: {
      customers: Array,
    },
  }
</script>

<style scoped>
</style>