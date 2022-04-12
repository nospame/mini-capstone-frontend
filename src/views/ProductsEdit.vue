<script>
import axios from 'axios';
export default {
  data: function () {
    return {
      message: "Welcome to Edit Product",
      editProductParams: {
        new_images: []
      },
      editProductImages: [],
      newProductImages: '',
      errors: []
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
          this.editProductParams = response.data;
          this.editProductImages = this.editProductParams.images;
        })
    },
    updateProduct: function (product) {
      this.editProductParams.new_images = this.newProductImages.split(', ');
      axios.patch(`/products/${product.id}.json`, this.editProductParams)
        .then(response => {
          console.log(response.data);
          this.$router.push(`/products/${product.id}`)
        })
        .catch(errors => {
          this.errors = errors.response.data.errors;
        })
    }
  }
};
</script>

<template>
  <div class="products-edit">
    <h1>{{ message }}</h1>
    <p v-for="error in errors">{{ errors }}</p>
    <div> Images:<br>
      <img v-for="image in editProductImages" v-bind:src="image.url" style="max-width: 85%">
    </div>
    <div> Add Images:
      <input type="text" v-model="newProductImages" placeholder="image1.jpg, image2.jpg">
    </div>
    <div> Name:
      <input type="text" v-model="editProductParams.name">
    </div>
    <div> Description:
      <input type="text" v-model="editProductParams.description">
    </div>
    <div> Price:
      <input type="text" v-model="editProductParams.price">
    </div>
    <button type="submit" v-on:click="updateProduct(editProductParams)">Submit</button>

  </div>
</template>

<style>
</style>