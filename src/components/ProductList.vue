<template>
    <div >
        <header> 
            <h2>Preview</h2>
        </header>
        <div class="headers">
            <h5 style="width: 20%;">Brand</h5>
            <h5 style="width: 20%;">Productname</h5>
            <h5 style="width: 60%;">Images</h5>
        </div>
        
        <div :key="index" v-for="(product, index) in products">
            <Product :product="product" />
        </div>

        
    </div>
</template>

<script>
import Product from './Product.vue'

export default {

    data() {
        return {
            items : [
                {brand: 'Vitra', product_name: 'Eames Lounge Chair', images: 'https://s3.eu-west-1.amazonaws.com/hungarian.phrasebook/decodata-frontend-assignment/images/vitra-eames-lounge-chair-met-ottoman-fauteuil-nieuwe-afmetingen-walnotenhout10.jpg'},
                {brand: 'Knoll', product_name: 'Barcelona', images: 'https://s3.eu-west-1.amazonaws.com/hungarian.phrasebook/decodata-frontend-assignment/images/Knoll-Barcelona-Chair-5.jpg'},
            ],
        }
    },
    props: ['products'],
    components: {
        Product
    }
    
}
</script>

<style scoped>
    header {
        display: flex;
        justify-content: start;
    }
    .brand-img {
        max-width: 100px;
    }
    .headers {
        display: flex;
        align-items: center;
        margin-top: 4rem;
    }
</style>
