<template>
    <div class="col-md-4 mb-4">
        <div class="card h-100">
            <img :src="imgUrl" class="card-img-top" :alt="title">
            <div class="card-body">
              <h5 class="card-title">{{ title }}</h5>
              <p class="card-text">{{ description }}</p>
              <p class="fw-bold text-primary">{{ price }}</p>
              <button class="btn btn-success w-100" @click.prevent="addToCart"> 加入購物車 </button>
            </div>
        </div>
     </div>

</template>
<script setup>
import { defineProps,defineEmits} from 'vue';
const props = defineProps({
    title:{type:String,required:true},
    description:{type:String,required:true},
    price:{type:Number,required:true},
    imgUrl:{type:String,required:true}
});
const emits = defineEmits(['add-to-cart']);
function addToCart(){
    emits('add-to-cart',{
        title:props.title,
        price:props.price
    });
}
</script>