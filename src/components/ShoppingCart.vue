<template>
    <div class="contenedor">
        <h1 class="mb-5">Carrito de Compras</h1>
        <b-container>
            <b-card>
            <ul>            
                <li v-for="product in products" :key="product.id">
                {{product.title}} - {{product.price | currency}} - {{product.quantity}}
                </li>                    
            </ul>
            <p><b>Total: {{total | currency}}</b></p>
            <b-button variant="primary" v-if="$store.state.cart.length !== 0" @click="$store.dispatch('checkout')">Checkout</b-button>
            <p v-if="$store.state.checkoutStatus">{{$store.state.checkoutStatus}}</p>
            </b-card>
        </b-container>
    </div>
</template>

<script>
    export default {
        computed: {
            products() {
               return this.$store.getters.cartProducts
            },
            total() {
               return this.$store.getters.cartTotal
            }
        }
    }
</script>

<style scoped>
    .contenedor {
        margin-top: 10px;
        padding: 10px;
        margin-bottom: 40px;
    }

    li {
        list-style-type: none;
    }
</style>