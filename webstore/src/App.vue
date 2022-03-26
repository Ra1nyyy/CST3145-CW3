<template>
  <div id="app">
    <header>
        <h1>{{sitename}}</h1>

        <!-- CHECKOUT BUTTON -->
        <div class="checkoutbut">
            <button @click='showCheckout'>
                {{this.cart.length}} Checkout
            </button>
        </div>
    </header>
    <product-list @addProduct='addToCart'></product-list>
    <checkout :cart='cart' @removeProduct='removeFromCart'></checkout>
  </div>
</template>

<script>
import productList from './components/productlist.vue'
import checkout from './components/checkout.vue'

export default {
  name: 'App',
  components: {
    productList,
    checkout
  },
  data() {
    return {
      sitename: "Vue.js Webstore",
      cart: [],
    }
  },
  methods: {
    showCheckout: function(){
      this.showProduct = this.showProduct ? false : true;
      },
      addToCart(product) {
        this.cart.push(product)
        product.availableInventory --
      },
      removeFromCart(product) {
        this.cart.forEach(product2 => {
          if (product2.id === product.id) {
            product.inventory ++
            this.cart.splice(this.cart.indexOf(product), 1)
          }
      });
    }
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
</style>
