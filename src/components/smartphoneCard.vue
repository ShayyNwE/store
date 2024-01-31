<template>
    <div class="smartphoneContainer">
        <img src="../assets/iphone.svg" @click="$emit('product-click', product)">
        <div class="product-title">{{ product.title }}</div>
    </div>
</template>
<script>
    export default {
        name:'smartphoneCard',
        props: {
            product: {
                type: Object,
                default: null
            }
        }
    }
</script>
<style scoped>

.smartphoneContainer{
    position: relative;
}

img{
    max-width: 200px;
    cursor: pointer;
}
.product-title{
    position: absolute;
    left: 40%;
    top: 50%;
    transform: translate(-50%, -50%);
    z-index: 100;

}
</style>