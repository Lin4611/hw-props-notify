<template>
    <div class="col-md-4 mb-4">
        <div class="card h-100">
            <img :src="product.imgUrl" class="card-img-top" :alt="product.title">
            <div class="card-body">
              <h5 class="card-title">{{ product.title }}</h5>
              <p class="card-text">{{ product.description }}</p>
              <p class="fw-bold text-primary">${{ product.price }}</p>
              <button class="btn btn-success w-100" @click.prevent="addToCart"> 加入購物車 </button>
            </div>
        </div>
     </div>
</template>
<script setup>
const props = defineProps({
    product:{type:Object,required:true}
});
const emits = defineEmits(['add-to-cart']);
function addToCart(){
    emits('add-to-cart',{
        title:props['product'].title,
        price:props['product'].price
    });
}
</script>