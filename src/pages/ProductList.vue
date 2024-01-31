<template>
    <div class="product-list">
        <template v-for="product in products">
        <component :is="product.component" :product="product" :key="product.id" :class="product.cssClass" @product-click="$emit('product-click' , $event)"></component>
        </template>
    </div>
</template>

<script>
import ProductCard from "../components/ProductCard.vue";
import smartphoneCard from "../components/smartphoneCard.vue";

export default{
    name: 'ProductList',
    emit:[
        'product-click'
    ],
    props:{
        products: {
            type: Object,
            default: null
        } 
    },
    components:{
        ProductCard,
        smartphoneCard
    }
}
</script>