<template>
    <div>
      <h2>Add Product</h2>
      <form @submit.prevent="addProduct">
        <label for="name">Name:</label>
        <input type="text" id="name" v-model="newProduct.name" required>
        <label for="description">Description:</label>
        <input type="text" id="description" v-model="newProduct.description" required>
        <label for="price">Price:</label>
        <input type="number" id="price" v-model.number="newProduct.price" required>
        <button type="submit">Add Product</button>
      </form>
    </div>
  </template>
  
  <script>
import swal from 'sweetalert';

  export default {
    name: 'AddProduct',
    data() {
      return {
        newProduct: {
          name: '',
          description: '',
          price: ''
        }
      }
    },
    methods: {
      addProduct() {
        const product = {
          id: Date.now(),
          name: this.newProduct.name,
          description: this.newProduct.description,
          price: parseFloat(this.newProduct.price)
        };
        this.$store.commit('addProduct', product);
        swal("Success!", "Product added successfully!", "success");
        this.$router.push({ name: 'ProductList' });
      }
    }
  }
  </script>
  