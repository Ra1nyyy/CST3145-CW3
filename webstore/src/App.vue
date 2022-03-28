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
    <product-list :products='products' @addProduct='addToCart'></product-list>
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
      products: [
        {
          id: 1,
          image: "math.png",
          subject: "Math",
          location: "China",
          price: 10,
          availableInventory: 5,
          rating: 5,
          inCart: 0
        },
      ],
    };
  },
  methods: {
    showCheckout: function(){
      this.showProduct = this.showProduct ? false : true;
      },
      addToCart(product) {
        let added = false;
        this.cart.forEach((product2) => {
          if (product2.id === product.id) {
            product.inCart++;
            added = true;
          }
        });
        if (!added) {
        this.cart.push(product)
        product.inCart = 1;
        }
        product.availableInventory --
      },
      removeFromCart(product) {
        this.cart.forEach(product2 => {
          if (product2.id === product.id) {
            product.availableInventory ++;
            product.inCart --;
            if (product.inCart == 0) {
            this.cart.splice(this.cart.indexOf(product), 1)
            }
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
