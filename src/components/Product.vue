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
        font-size: 10px;
    }
    .product-row p {
        width: 20%;
        font-size: 10px;
    }
    .product-images {
        height: 60%;
        max-width: 100px;
        max-height: 100px;
    }
    .images-div {
        display: flex;
        flex-direction: column;
        width: 60%;
    }

    @media (min-width: 600px) {
        .product-row h5 {
            font-size: 14px;
        }
        .product-row p {
            font-size: 14px;
        }
        .images-div {
            flex-direction: row;
            justify-content: center;
        }
    }
</style>
