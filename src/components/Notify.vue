<template>
    <div class="position-fixed top-0 end-0 p-3" style="z-index: 1050">
        <div class="toast show align-items-center text-white bg-success border-0">
        <div class="d-flex">
            <div class="toast-body">
                {{ message }}
            </div>
            <button type="button" class="btn-close btn-close-white me-2 m-auto" @click.prevent="clearMsg"></button>
        </div>
        </div>
    </div>
</template>
<script setup>
import { inject,defineEmits } from 'vue';
const message = inject('message');
const emits = defineEmits(['clear-msg'])
const clearMsg =()=>{
    emits('clear-msg')
}

</script>