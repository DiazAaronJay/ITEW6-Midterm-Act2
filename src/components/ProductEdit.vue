<template>
    <div class="product-list">
      <div class="list-header">
        <h2>Product List</h2>
        <button class="add-button" @click="addProduct(product)">
          <span class="add-icon">+</span> Add Product
        </button>
      </div>
      <br >
      <transition-group name="fade">
        <div class="product-grid">
          <div v-for="product in products" :key="product.id" class="product-item">
            <div class="product-card">
              <img :src="product.image" alt="Product Image" class="product-image" />
              <div class="product-info">
                <h3>{{ product.name }}</h3>
                <p>{{ product.description }}</p>
                <p>Price: ${{ product.price }}</p>
                <div class="button-container">
                  <button class="edit-btn" @click="editProduct(product)">Edit</button>
                  <button class="delete-btn" @click="confirmDelete(product.id)">Delete</button>
                </div>
              </div>
            </div>
          </div>
        </div>
      </transition-group>
      </div>
  </template>
  
  <script>
  import Swal from 'sweetalert2';
  
  export default {
    name: 'ProductList',
    props: {
      products: {
        type: Array,
        required: true,
      },
    },
    methods: {
      addProduct() {
        Swal.fire({
          title: 'Add Product',
          html: `
            <input id="name" class="swal2-input" placeholder="Name">
            <input id="description" class="swal2-input" placeholder="Description">
            <input id="price" class="swal2-input" placeholder="Price">
          `,
          showCancelButton: true,
          confirmButtonText: 'Add Product',
          cancelButtonText: 'Cancel',
          preConfirm: () => {
            const name = Swal.getPopup().querySelector('#name').value;
            const description = Swal.getPopup().querySelector('#description').value;
            const price = parseFloat(Swal.getPopup().querySelector('#price').value);
            if (!name || !description) {
              Swal.showValidationMessage('Please Enter a Name or Description');
              return false;
            }
            if (isNaN(price)) {
              Swal.showValidationMessage('Please Enter a Price or valid Price');
              return false;
            }
            return { name, description, price };
          }
        }).then((result) => {
          if (result.isConfirmed) {
            const { name, description, price } = result.value;
            const id = this.products.length + 1;
            const image = 'images/default.png'; 
            const newProduct = { id, name, description, price, image };
            this.$emit('add-product', newProduct);
            Swal.fire({
              title: 'Product Added!',
              icon: 'success',
            });
          }
        });
      },
      editProduct(product) {
        Swal.fire({
          title: 'Edit Product',
          html: `
            <input id="name" class="swal2-input" placeholder="Name" value="${product.name}">
            <input id="description" class="swal2-input" placeholder="Description" value="${product.description}">
            <input id="price" class="swal2-input" placeholder="Price" value="${product.price}">
          `,
          showCancelButton: true,
          confirmButtonText: 'Save Changes',
          cancelButtonText: 'Cancel',
          preConfirm: () => {
            const name = Swal.getPopup().querySelector('#name').value;
            const description = Swal.getPopup().querySelector('#description').value;
            const price = parseFloat(Swal.getPopup().querySelector('#price').value);
            if (!name || !description) {
              Swal.showValidationMessage('Please Enter a Name or Description');
              return false;
            }
            if (isNaN(price)) {
              Swal.showValidationMessage('Please Enter a Price or valid Price');
              return false;
            }
            return { name, description, price };
          }
        }).then((result) => {
          if (result.isConfirmed) {
            const { name, description, price } = result.value;
            product.name = name;
            product.description = description;
            product.price = price;
            this.$emit('update-product', product);
            Swal.fire({
              title: 'Changes saved!',
              icon: 'success',
            });
          }
        });
      },
      confirmDelete(productId) {
        Swal.fire({
          title: 'Are you sure?',
          text: 'You won\'t be able to revert this!',
          icon: 'warning',
          showCancelButton: true,
          confirmButtonColor: '#d33',
          cancelButtonColor: '#3085d6',
          confirmButtonText: 'Yes, delete it!'
        }).then((result) => {
          if (result.isConfirmed) {
            this.deleteProduct(productId);
          }
        });
      },
      deleteProduct(productId) {
        this.$emit('delete-product', productId);
      },
    },
  };
  </script>
  
  <style scoped>
  .product-list {
    margin-top: 20px;
  }
  
  .list-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
  
  .list-header h2 {
    font-size: 28px;
  }
  
  .add-button {
    padding: 8px 16px;
    background-color: #0E46A3;
    color: #fff;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    display: flex;
    align-items: center;
  }
  
  .add-button:hover {
    background-color: #0056b3;
  }
  
  .add-icon {
    font-size: 24px;
    margin-right: 5px;
  }
  
  .product-grid {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    gap: 20px;
  }
  
  .product-item {
    cursor: pointer;
  }
  
  .product-card {
    display: flex;
    align-items: center;
    padding: 15px;
    background-color: #f0f0f0;
    border-radius: 10px;
    box-shadow: 5px 5px 10px #bebebe, -5px -5px 10px #ffffff;
    transition: transform 0.3s ease;
  }
  
  .product-card:hover {
    transform: scale(1.01);
  }
  
  .product-image {
    width: 100px;
    height: 100px;
    object-fit: contain;
    margin-right: 20px;
  }
  
  .product-info {
    flex: 1;
  }
  
  .button-container {
    display: flex;
    justify-content: flex-end;
  }
  
  .edit-btn,
  .delete-btn {
    padding: 8px 16px;
    margin-left: 10px;
    border: none;
    border-radius: 5px;
    color: #fff;
    cursor: pointer;
    transition: background-color 0.3s ease;
  }
  
  .edit-btn {
    background-color: #0E46A3;
  }
  
  .delete-btn {
    background-color: #e05a3f;
  }
  
  .edit-btn:hover {
    background-color: #3fa8e0;
  }
  
  .delete-btn:hover {
    background-color: #c7391d;
  }
  
  .fade-enter-active,
  .fade-leave-active {
    transition: opacity 0.5s;
  }
  
  .fade-enter,
  .fade-leave-to {
    opacity: 0;
  }
  </style>