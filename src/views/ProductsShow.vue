<script>import axios from "axios";

export default {
  data: function () {
    return {
      message: "Welcome to the Product Show",
      product: {}
    };
  },
  created: function () {
    this.showProduct();
  },
  methods: {
    showProduct: function () {
      axios.get(`/products/${this.$route.params.id}.json`)
        .then(response => {
          console.log(response.data);
          this.product = response.data;
        })
    }
  },
};
</script>

<template>
  <div class="products-show">
    <h1>{{ message }}</h1>
    <img v-bind:src="product.images[0].url" style="max-width: 85%">
    <h2>{{ product.name }}</h2>
    <p>{{ product.description }}</p>
    <p>Price: ${{ product.price }}</p>
    <p>Tax: ${{ product.tax }}</p>
    <p>Total: ${{ product.total }}</p>
  </div>
</template>

<style>
</style>