<template>
  <div id="app">
    
    <!--<div>
      <label>Mots clés</label> <input type="text" v-model="keywords">
    </div>
    -->
    <ProductList :products="filteredProducts" @product-click="onProductClick($event)"/>
    
    <div v-if="displayPopup === true" class="product-popup">
      <button @click="onPopupClose" class="popup-close-button">x</button>
      <productDetails :product="displayedProduct"></productDetails>
    </div>
  
  </div>
</template>

<script>
import axios from "axios";
import productDetails from "./components/productDetails.vue";
import ProductList from "./pages/ProductList.vue";

export default {
  name: 'App',
  components: {
    productDetails,
    ProductList
  },
  data() {
    return {
      products:[],
      keywords: '',
      displayPopup: false,
      displayedProduct: null
    }
  },
  computed: {
    filteredProducts(){
      return this.products.filter(product => {
        return product.title.toLowerCase().includes(this.keywords.toLowerCase())
      });
    }
  },
  methods: {
    getProducts(){
      axios.get('https://dummyjson.com/product')
      .then((Response) => {
        const apiProducts = Response.data.products;
        const vueProducts = apiProducts.map(product =>{
          if(product.category === 'smartphones') {
            product.component = 'smartphoneCard';
            product.cssClass = 'smartphone-card';
          } else{
            product.component = 'productCard';
            product.cssClass = 'product-card';
          }

          return product;
        });
        this.products =vueProducts; 
      });
    },
    getProductComponent(product){
      if (product.category === 'smartphones'){
        return 'smartphoneCard'
      }
      return 'productCard'
    },

    getProductClass(product){
      if(product.category === 'smartphones'){
        return 'smartphone-card'
      }
      return 'product-card'
    },
    wait(timeout){
      return new Promise((resolve)=>{
        setTimeout(()=>{resolve()},timeout);
      })
    },
    onProductClick(product) {
    this.displayedProduct=product;
    this.displayPopup =true;
    },
    onPopupClose() {
      this.displayPopup = false;
    }
  },
  mounted(){
    this.getProducts();
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.product-list{
  display: flex;
  flex-wrap: wrap;
  gap: 20px;
  justify-content: center;
}

.product-card{
  width:200px;
  height: 300px;
}

.smartphoneCard{
  max-width: 200px;
}

.product-popup{
  position: absolute;
  width: 800px;
  height: 700px;
  z-index: 100;
  top: 50%;
  left: 50%;
  background-color: rgb(255, 255, 255);
  border: 1px solid black;
  border-radius: 10px;
  transform: translate(-50%, -50%);
}

.popup-close-button{
  float: right;
  width: 20px;
  height: 20px;
}
</style>
