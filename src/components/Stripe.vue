<template>
  <div id="root">
    <h2>Stripe Integration</h2>
    <h2>Create Customer</h2>
    <a href="http://localhost:4500/createCustomer">Create Customer</a> <br />
    <br />
    <button @click="getCheckOutURL">Proceed</button>
    <p>loading: {{ loading }}</p>
    <a v-if="checkOutState" :href="checkoutURL">Checkout</a>
  </div>
</template>

<script>
import axios from 'axios';
export default {
  name: 'Stripe',
  data() {
    return {
      loading: false,
      checkOutState: false,
      checkoutURL: '',
    };
  },
  methods: {
    async getCheckOutURL() {
      try {
        this.loading = true;
        let {
          data: { data },
        } = await axios.get('http://localhost:4500/createSession');
        console.log(data);
        this.loading = false;
        this.checkoutURL = data.url;
        this.checkOutState = true;
      } catch (error) {
        console.log(error);
      }
    },
  },
  computed: {},
  // LifeCycle Hook
  created() {},
};
</script>

<style></style>
