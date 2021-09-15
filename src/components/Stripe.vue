<template>
  <div id="root">
    <h2>Stripe Integration</h2>
    <h2>Create Customer</h2>
    <a href="http://localhost:4500/createCustomer">Create Customer</a> <br />
    <br />
    <div>
      <h2>Content On Modal</h2>
      <button v-if="!checkOutState" @click="getCheckOutURL">Proceed</button>
      <p>loading: {{ loading }}</p>
    </div>
    <a v-if="checkOutState" :href="checkoutURL">Checkout</a>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "Stripe",
  data() {
    return {
      loading: false,
      checkOutState: false,
      checkoutURL: "",
      customerId: "cus_KEQSB9qf9Mf4oc",
      priceId: "price_1JZdjbSIUZLasS08kBQn7HEl",
    };
  },
  methods: {
    async getCheckOutURL() {
      try {
        this.loading = true;
        let {
          data: { data },
        } = await axios.get(
          `http://localhost:4500/createSession?customerId=${this.customerId}&priceId=${this.priceId}`
        );
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
