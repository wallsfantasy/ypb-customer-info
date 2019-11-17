<template>
  <div id="customer-form">
    <div v-if="validationErrors.length">
      <p>
        <b>Please correct the following error(s):</b>
      </p>
      <ul>
        <li v-for="(error, index) in validationErrors" :key="index">{{ error }}</li>
      </ul>
    </div>

    <form @submit.prevent="handleSave">
      <div class="container">
        <button type="button" @click="handleAdd" class="btn btn-primary btn-block">Add Customer</button>
        <button type="submit" class="btn btn-success btn-block">Save</button>
      </div>

      <div :id="`customer-${index}`" class="container bg-light customer" v-for="(customer, index) in customers" :key="index">
        <!-- name -->
        <div class="form-group row">
          <label :for="`name-${index}`" class="col-sm-2">Name</label>
          <div class="col-sm-10">
            <input :id="`name-${index}`" class="form-control" v-model="customer.name" type="text" placeholder="Name"/>
          </div>
        </div>

        <!-- email -->
        <div class="form-group row">
          <label :for="`email-${index}`" class="col-sm-2">Email</label>
          <div class="col-sm-10">
            <input :id="`email-${index}`" class="form-control" v-model="customer.email" type="text" placeholder="E-mail"/>
          </div>
        </div>

        <!-- juices -->
        <div class="form-group row">
          <div class="col-sm-2">Favourite juices..</div>
          <div class="col-sm-10">
            <div class="form-check">
              <input :id="`juice-apple-${index}`" class="form-check-input" v-model="customer.juices" type="checkbox" name="juices" value="apple">
              <label :for="`juice-apple-${index}`" class="form-check-label">Apple</label>
            </div>
            <div class="form-check">
              <input :id="`juice-grape-${index}`" class="form-check-input" v-model="customer.juices" type="checkbox" name="juices" value="grape">
              <label :for="`juice-grape-${index}`" class="form-check-label">Grape</label>
            </div>
            <div class="form-check">
              <input :id="`juice-melon-${index}`" class="form-check-input" v-model="customer.juices" type="checkbox" name="juices" value="melon">
              <label :for="`juice-melon-${index}`" class="form-check-label">Melon</label>
            </div>
            <div class="form-check">
              <input :id="`juice-orange-${index}`" class="form-check-input" v-model="customer.juices" type="checkbox" name="juices" value="orange">
              <label :for="`juice-orange-${index}`" class="form-check-label">Orange</label>
            </div>
          </div>
        </div>
      </div>
    </form>
  </div>
</template>

<script>
  export default {
    name: "CustomerForm",
    data() {
      return {
        validationErrors: [],
        customers: [],
      }
    },
    methods: {
      handleAdd() {
        this.customers.push({name: '', email: '', juices: []});
      },
      handleSave() {
        this.validationErrors = [];

        // validate
        this.customers.forEach((cus, idx) => {
          if (cus.name === null || cus.name === '') {
            this.validationErrors.push(`${idx}: Name required.`);
          }
          if (cus.email === null || cus.email === '') {
            this.validationErrors.push(`${idx}: Email required.`);
          }
          if (cus.juices.length === 0) {
            this.validationErrors.push(`${idx}: At lease one juice required.`);
          }
        });

        if (this.validationErrors.length) {
          return;
        }

        // emit add:customer if validation passed
        this.customers.forEach((cus) => {
          this.$emit('add:customer', cus);
        });

        // reset form
        this.customers = [];

      },
    },
  }
</script>

<style scoped>
  form .container {
    margin: 2em 0 2em;
  }
  form .customer {
    padding: 1em 2em 1em;
  }
</style>