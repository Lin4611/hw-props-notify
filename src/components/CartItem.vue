<template>
    <li class="list-group-item d-flex justify-content-between align-items-center">
        <div>
            <h6 class="my-0">{{ cartitem.title }}</h6>
            <small class="text-muted">數量：{{cartitem.count}}</small>
        </div>
        <div>
            <span class="text-muted">$ {{cartitem.price*cartitem.count}} </span>
            <button class="btn btn-sm btn-outline-danger ms-2" @click.prevent="delCartItem"> 移除 </button>
        </div>
    </li>
</template>
<script setup>
const props = defineProps({
    cartitem:{type:Object,required:true}
});
const emits =defineEmits(['del-cart-item']);
const delCartItem =()=>{
    emits('del-cart-item',props['cartitem'].id)
}
</script>