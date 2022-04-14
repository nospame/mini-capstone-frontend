<script>import axios from "axios";

export default {
  data: function () {
    return {
      message: "Welcome to the Products Index",
      products: [],
      searchTerm: ''
    };
  },
  created: function () {
    this.indexProducts();
  },
  methods: {
    indexProducts: function () {
      axios.get('/products.json')
        .then(response => {
          console.log(response.data);
          this.products = response.data;
        })
    },
    filterProducts: function () {
      return this.products.filter(product => {
        let lowerName = product.name.toLowerCase();
        let lowerSearchTerm = this.searchTerm.toLowerCase();
        return lowerName.includes(lowerSearchTerm);
      })
    }
  },
};
</script>

<template>
  <div class="products-index">
    <h1>{{ message }}</h1>
    Search: <input type="text" v-model="searchTerm">
    <p>
      <router-link to="/products/new">Add a New Product</router-link>
    </p>
    <div v-for="product in filterProducts()">
      <img v-bind:src="product.images[0].url" style="max-width: 85%">
      <h3>{{ product.name }}</h3>
      <p>${{ product.price }}</p>
      <router-link v-bind:to="`/products/${product.id}`">More Info</router-link>
      <hr>
    </div>

  </div>
</template>

<style>
</style>