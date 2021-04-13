<template>
    <b-container>
        <h1 class="mb-5">Lista de Productos</h1>
        <img 
            v-if="loading"
            src="https://1.imgur.com/JfPpwOA.gif" 
        >
        <b-container v-else>
            <ul class="products-items">                           
                <b-card 
                v-for="product in products" 
                :key="product.id"
                :title="product.title"
                :img-src="product.img"
                img-top
                :img-height="300"
                :img-width="150"
                style="max-width:20rem"
                >
                {{product.price | currency}} - {{product.inventory}} unidades en stock
                <b-button variant="primary mt-3"
                 @click="addProductToCart(product)">Agregar al carrito</b-button>
                </b-card>                   
            </ul>
        </b-container>        
    </b-container>
</template>

<script>

    export default {
        data() {
            return {
                loading: false
            }
        },

        computed: {
            products () {
                return this.$store.getters.availableProducts
            }
        },

        methods: {
            addProductToCart(product) {
                this.$store.dispatch('addProductToCart', product)
            }
        },

        created() {
            this.loading = true
            this.$store.dispatch('fetchProducts')
                .then(() => this.loading = false )
        }
    }
</script>

<style scoped>
    .products-items {
        display: flex;
        flex-direction: row;
        justify-content: space-around;
        flex-wrap: wrap;
    }

    li {
        list-style-type: none;
    }
</style>