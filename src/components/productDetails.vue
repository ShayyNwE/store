<template>
    <div class="product-container">
        <h2>{{ product.title }}</h2>
        <img :src="product.thumbnail">
        <div class="product-data">
            <div class="product-data-row">
                <label>Référence: </label><span>{{ product.id }}</span>
            </div>
            <div class="product-data-row">
                <label>Marque: </label><span>{{ product.brand }}</span>
            </div>
            <div class="product-data-row">
                <label>Catégorie: </label><span>{{ product.category }}</span>
            </div>
            <div class="product-data-row">
                <label>Déscription: </label><span>{{ product.description }}</span>
            </div>
            <div class="product-data-row">
                <label>évaluation client </label><ProgressBar :max="5" :value="product.rating"></ProgressBar>
            </div>
        </div>
    </div>

</template>
<script>
import ProgressBar from './ProgressBar.vue';
export default{
    name: 'productDetails',
    components: {
        ProgressBar
    },
    props: {
        product: {
            type:Object,
            default: null
        }
    }
}
</script>
<style>
.product-container{
    display: flex;
    flex-direction: column;
}
.product-data{
    display: flex;
    flex-direction: column;
}
.product-data-raw{
    display: flex;
    justify-content: space-between;
}
</style>