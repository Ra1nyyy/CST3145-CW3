<template>
    <main>
        <div v-for="product in products" :key="product.id">
            <figure>
                <img v-bind:src="product.image"/>
            </figure>
            <h2>{{product.subject}}</h2>
            <p>Location: {{product.location}}</p>
            <p>Price: {{product.price}}</p>
            <p>Available stock: {{product.availableInventory}}</p>
            <p>Rating: {{product.rating}}</p>
            <button @click="addToCart(product)">Add to cart</button>
        </div>
    </main>
</template>

<script>

 export default {
     name: "ProductList",
     props: ['products'],
     data() {
         return {}
     },
     methods: {
         addToCart(product) {
            this.$emit('addProduct', product);
         },
     },
 };

</script>

