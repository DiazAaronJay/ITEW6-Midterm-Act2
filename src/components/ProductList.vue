<template>
  <div class="product-list">
    <div class="list-header">
      <h2>Product List</h2>
      <button class="add-button">
        <span class="add-icon">+</span> Add Product
      </button>
    </div>
    <div class="product-grid">
      <div v-for="product in products" :key="product.id" class="product-item">
        <div class="product-card">
          <img :src="product.image" alt="Product Image" class="product-image" />
          <div class="product-info">
            <h3>{{ product.name }}</h3>
            <p>{{ product.description }}</p>
            <p>Price: ${{ product.price }}</p>
            <div class="button-container">
              <button class="edit-btn">Edit</button>
              <button class="delete-btn">Delete</button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ProductList',
  props: {
    products: {
      type: Array,
      required: true,
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
</style>
