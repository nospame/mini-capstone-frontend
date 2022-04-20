<script>import axios from "axios";

export default {
  data: function () {
    return {
      message: "Shop",
      cartedProducts: []
    };
  },
  created: function () {
    this.getCartedProducts()
  },
  methods: {
    getCartedProducts: function () {
      axios.get('/carted_products.json')
        .then(response => {
          console.log(response.data)
          this.cartedProducts = response.data
          this.message = this.cartedProducts.length === 0 ? "Shopping Cart is Empty" : "Shopping Cart"
        })
    },
    updateCartedProduct: function (cartedProduct) {
      axios.patch(`/carted_products/${cartedProduct.id}.json`, cartedProduct)
        .then(response => {
          console.log(response.data)
          this.$router.go(0)
        })
    },
    removeCartedProduct: function (cartedProduct) {
      cartedProduct.status = "removed"
      axios.patch(`/carted_products/${cartedProduct.id}.json`, cartedProduct)
        .then(response => {
          console.log(response.data)
          this.$router.go(0)
        })
    }

  },
};
</script>
<!-- frontend needs to send update request to backend -->
<template>
  <div class="home">
    <h1>{{ message }}</h1>

    <div v-for="cartedProduct in cartedProducts">
      <img v-bind:src="cartedProduct.images[0].url" style="max-width: 85%"><br />
      {{ cartedProduct.product.name }}<br />
      <input type="number" v-model="cartedProduct.quantity">
      <button v-on:click="updateCartedProduct(cartedProduct)">Update Quantity</button> <br />
      <button v-on:click="removeCartedProduct(cartedProduct)">Remove from Cart</button><br />
      ${{ cartedProduct.price }}
      <hr>

    </div>
  </div>
</template>

<style>
</style>