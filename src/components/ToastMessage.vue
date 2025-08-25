<template>
    <div class="position-fixed top-0 end-0 p-3" style="z-index: 1050">
        <div class="toast show align-items-center text-white bg-success border-0" v-for="m in messages" :key="m.id">
        <div class="d-flex">
            <div class="toast-body">
                {{ m.text }}
            </div>
            <button type="button" class="btn-close btn-close-white me-2 m-auto" @click.prevent="clearMsg(m.id)"></button>
        </div>
        </div>
    </div>
</template>
<script setup>
import { inject } from 'vue';
const messages = inject('messages');
const emits = defineEmits(['clear-msg'])
const clearMsg =(id)=>{
    emits('clear-msg',id)
}

</script>