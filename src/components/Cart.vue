<template>
    <li class="list-group-item d-flex justify-content-between align-items-center">
        <div>
            <h6 class="my-0">{{ title }}</h6>
            <small class="text-muted">數量：{{count}}</small>
        </div>
        <div>
            <span class="text-muted">{{price*count}}</span>
            <button class="btn btn-sm btn-outline-danger ms-2" @click.prevent="delCartItem"> 移除 </button>
        </div>
    </li>
</template>
<script setup>
import { defineProps,defineEmits } from "vue";
const props = defineProps({
    id:{type:Number,required:true},
    title:{type:String,required:true},
    price:{type:Number,required:true},
    count:{type:Number,required:true}
});
const emits =defineEmits(['del-cart-item']);
const delCartItem =()=>{
    emits('del-cart-item',props.id)
}
</script>