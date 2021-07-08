<template>
    <div class="product-row">
        <h5>{{product.brand}}</h5>
        <p>{{product.product_name}}</p>
        <div class="images-div">
            <div :key="index" v-for="(image, index) in product.images">
                <b-img fluid class="product-images" :src='image.url' alt="anyt" ></b-img>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'Product',
    props: ['product'],
}
</script>

<style scoped>
    .product-row {
        display: flex;
        align-items: center;
        justify-content: space-evenly;
    }
    .product-row h5 {
        width: 20%;
    }
    .product-row p {
        width: 20%;
    }
    .product-images {
        height: 60%;
        max-width: 100px;
        max-height: 100px;
    }
    .images-div {
        display: flex;
        width: 60%;
    }
</style>
