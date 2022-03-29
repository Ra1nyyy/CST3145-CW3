<template>
  <div id="app">
    <header>
        <h1>{{sitename}}</h1>

      <!-- CHECKOUT BUTTON -->
      <div class="checkOutBut">
        <button @click='showCheckout'>
          {{this.cart.length}} Checkout
        </button>
      </div>

      <!-- SORT BUTTONS -->
      <div class="sort">
        <p>Sort by:
            <button @click="sortedPriceHigh">Price: High to Low</button>
            <button @click="sortedPriceLow">Price: Low to High</button>
            <button @click="sortedRatingsHigh">Avg. Customer Review</button>
        </p>
      </div>

      <!-- SEARCH BAR -->
      <input type="text" v-model="search" id="search" placeholder="Search..">

        
    </header>
    <div v-if='showProduct'>
      <product-list :products='products' @addProduct='addToCart'></product-list>
    </div>
    <div v-else>
      <checkout :cart='cart' @removeProduct='removeFromCart'></checkout>
    </div>
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
      sitename: "After School Club",
      cart: [],
      showProduct: true,
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
        {
          id: 2,
          image: "english.jpg",
          subject: "English",
          location: "USA",
          price: 120,
          availableInventory: 5,
          rating: 2,
          inCart: 0
        },
        {
          id: 3,
          image: "science.png",
          subject: "Science",
          location: "Tokyo",
          price: 77,
          availableInventory: 5,
          rating: 4,
          inCart: 0
        },
        {
          id: 4,
          image: "history.jpg",
          subject: "History",
          location: "Germany",
          price: 83,
          availableInventory: 5,
          rating: 2,
          inCart: 0
        },
        {
          id: 5,
          image: "geo.jpg",
          subject: "Geography",
          location: "Africa",
          price: 33,
          availableInventory: 5,
          rating: 3,
          inCart: 0
        },
        {
          id: 6,
          image: "dandt.jpg",
          subject: "Design and Technology",
          location: "Califfornia",
          price: 16,
          availableInventory: 5,
          rating: 4,
          inCart: 0
        },
        {
          id: 7,
          image: "art.jpg",
          subject: "Art and Design",
          location: "London",
          price: 50,
          availableInventory: 5,
          rating: 1,
          inCart: 0
        },
        {
          id: 8,
          image: "music.jpg",
          subject: "Music",
          location: "Korea",
          price: 99,
          availableInventory: 5,
          rating: 0,
          inCart: 0
        },
        {
          id: 9,
          image: "pe.jpg",
          subject: "Physical Education",
          location: "Jamaica",
          price: 100,
          availableInventory: 5,
          rating: 5,
          inCart: 0
        },
        {
          id: 10,
          image: "computing.jpg",
          subject: "Computing",
          location: "Philippines",
          price: 72,
          availableInventory: 5,
          rating: 2,
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
    },
    // sortedPriceLow: function(){
    //     function compare(a,b){
    //         if (a.price > b.price) return 1
    //         if (a.price < b.price) return -1
    //         return 0
    //     }
    //     return this.products.sort(compare)
    // },
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
#productLists {
    box-sizing: border-box;
  }
  .sort {
    padding-right: 70%;
    /* display: inline-block; */
    font-size: 20px;
    /* background-color: #2c3e50; */
}
.checkOutBut {
  padding-left: 90%;
  background-color: aqua;
}
</style>
