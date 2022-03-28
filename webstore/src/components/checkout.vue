<template>
    <div>
        <h2>Checkout</h2>
        <h3>Added products</h3>
        <div v-for='product in cart' :key="product.id">
            <h3>{{product.subject}}</h3> Quantity: {{product.inCart}}
            <button @click="removeProduct(product)">remove</button>
        </div>
        <p>
            <strong>Name</strong> <input v-model="name"/>
            <strong>Address</strong> <input v-model="address"/>
            <button>Submit</button>
        </p>
    </div>
</template>

<script>
export default {
    name: "CheckOut",
    props: ['cart'],
    data() {
        return {
            name: "",
            address: "",
        };
    },
    methods: {
        removeProduct(product) {
            this.$emit('removeProduct', product)
        }
    }
};
</script>