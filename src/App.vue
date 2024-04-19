<template>
  <<<<<<< HEAD
  <div id="app">
    <header class="sticky-header">
      <h1>Product Management</h1>
    </header>
    <main>
      <div class="container-fluid">
        <div class="row">
          <div class="hero-section">
            <img src="images/hero-bg.png" alt="Hero Image" />
            <div class="hero-text">
              <h2>Find Your Next Favorite Piece!</h2>
            </div>
          </div>
        </div>
        <div class="row">
          <ProductList :products="products" @add-product="addProduct" @delete-product="deleteProduct" />
        </div>
      </div>
    </main>
  </div>
</template>

<script>
import ProductList from './components/ProductList.vue';

export default {
  name: 'App',
  components: {
    ProductList,
  },
  data() {
    return {
      products: [
        { id: 1, name: 'Merch A', description: 'Hoodie Jacket HunterxHunter', price: 470.00, image: 'images/merch1.webp' },
        { id: 2, name: 'Merch B', description: '3 Piece One Piece Set Figures', price: 1190.00, image: 'images/merch2.png' },
        { id: 3, name: 'Merch C', description: 'Dragon Ball Figure', price: 1099.00, image: 'images/merch3.png' },
        { id: 4, name: 'Merch D', description: 'Attack on Titan Corps Flag necklace', price: 150.00, image: 'images/merch4.png' },
        { id: 5, name: 'Merch E', description: 'One Piece Black Bag', price: 499.00, image: 'images/merch5.png' },
        { id: 6, name: 'Merch F', description: 'Demon Slayer Stickers', price: 60.00, image: 'images/merch6.png' },
        { id: 7, name: 'Merch G', description: 'Death Note Notebook', price: 49.00, image: 'images/merch7.png' },
        { id: 8, name: 'Merch H', description: 'Gojo Satoru keychain', price: 35.00, image: 'images/merch8.png' },
        { id: 9, name: 'Merch I', description: 'Fruit Basket Merch Bundle', price: 69.00, image: 'images/merch9.png' },
        { id: 10, name: 'Merch J', description: 'MHA Sticker Bundle', price: 120.00, image: 'images/merch10.png' },
      ],
    };
  },
  methods: {
    addProduct(newProduct) {
      this.products.push(newProduct);
    },
    deleteProduct(productId) {
      this.products = this.products.filter(product => product.id !== productId);
    },
  },
};
</script>

<style>
header {
  background-color: #1C1678;
  color: #fff;
  padding: 5px;
  text-align: center;
  height: 40px;
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  z-index: 1000; 
}

header h1 {
  font-size: 18px;
}

main {
  width: 100%;
  margin-top: 50px;
}

.hero-section {
  width: 100%;
  height: 40vh;
  position: relative;
}

.hero-section img {
  width: 100%;
  height: 40vh;
}

.hero-text {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  text-align: center;
  color: #fff;
  font-size: 30px;
  font-variant: small-caps;
}
</style>
