<template>
  <div id="app" class="container">
    <h1>Customers</h1>
    <customer-form @add:customer="addCustomer"/>
    <customer-list :customers="customers"/>
  </div>
</template>

<script>
  import CustomerList from '@/components/CustomerList'
  import CustomerForm from "@/components/CustomerForm";

  export default {
    name: 'app',
    components: {
      CustomerList,
      CustomerForm
    },
    data() {
      return {
        errors: [],
        customers: [
          {
            id: 1,
            name: 'Customer 1',
            email: 'customer1@example.com',
            juices: [
              'grape', 'orange', 'melon'
            ]
          },
          {
            id: 2,
            name: 'Customer 2',
            email: 'customer2@example.com',
            juices: [
              'apple', 'grape'
            ]
          },
        ]
      }
    },
    methods: {
      addCustomer(customer) {
        // increment id from latest customer
        const lastId =
            this.customers.length > 0
                ? this.customers[this.customers.length - 1].id
                : 0;
        const id = lastId + 1;
        const newCustomer = {...customer, id};

        this.customers = [...this.customers, newCustomer]
      }
    }
  }
</script>

<style>
</style>
