<script setup>
import { ref,computed, provide } from 'vue';
import ProductItem from './components/ProductItem.vue';
import Cart from './components/Cart.vue';
import Notify from './components/Notify.vue';
  const datas=ref([
    {
      title:'耳罩式藍牙耳機',
      description:'舒適配戴，支援降噪技術',
      price:2490,
      imgUrl:'https://images.unsplash.com/photo-1546435770-a3e426bf472b?q=80&amp;w=2065&amp;auto=format&amp;fit=crop&amp;ixlib=rb-4.1.0&amp;ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D'
    },{
    title: '無線滑鼠',
    description: '人體工學設計，支援多裝置連線',
    price: 890,
    imgUrl: 'https://images.unsplash.com/photo-1707592691247-5c3a1c7ba0e3?q=80&w=2070&auto=format&fit=crop&ixlib=rb-4.1.0&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D'
  },
  {
    title: '智慧手錶',
    description: '心率監測、運動追蹤、防水設計',
    price: 4990,
    imgUrl: 'https://images.unsplash.com/photo-1715420078667-e3e1cae7959c?q=80&w=687&auto=format&fit=crop&ixlib=rb-4.1.0&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D'
  },
  {
    title: '行動電源',
    description: '10000mAh 大容量，支援快充',
    price: 1290,
    imgUrl: 'https://images.unsplash.com/photo-1644571669401-9ab344866592?q=80&w=1170&auto=format&fit=crop&ixlib=rb-4.1.0&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D'
  },
  {
    title: '藍牙喇叭',
    description: '高音質輸出，支援防水設計',
    price: 1990,
    imgUrl: 'https://images.unsplash.com/photo-1754142927775-8f1e97ebd030?q=80&w=1074&auto=format&fit=crop&ixlib=rb-4.1.0&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D'
  }
  ]);
  const cart=ref([]);
  const message=ref('');
  provide('message',message);
  const notifystate=(msg)=>{
    message.value = msg;
    setTimeout(()=>{
      message.value='';
    },3000)
  }
  const handleAddToCart=(itemtitle,itemprice)=>{
    notifystate(`${itemtitle}已加入購物車`);
    if(cart.value.find(item=>item.title===itemtitle)){
      const index=cart.value.findIndex(item=>item.title===itemtitle);
      cart.value[index].count+=1;
    }else{
      cart.value.push({
      id:new Date().getTime(),
      title:itemtitle,
      price:itemprice,
      count: 1
    });
    }
  };
  const sum =computed(()=>{
    return cart.value.length >= 1 ? cart.value.reduce((pre,item)=>pre+item.price*item.count,0) : 0
  });
  const handleDelItem = (id)=>{
    const index = cart.value.findIndex(item=>item.id === id)
    if (cart.value[index].count>1)
    {
      cart.value[index].count-=1;
    }else{
      cart.value.splice(index,1);
    }
  }
const clearMessage = () =>{
    message.value='';
}

</script>

<template>
<div id="app" class="container py-4">
  <div class="row">
    <!-- 商品列表區 -->
     <div class="col-md-8">
      <h2 class="mb-3">商品列表</h2>
      <div class="row">
        <ProductItem  v-for="(item,index) in datas" 
          :key="index"
          :title="item.title"
          :description="item.description"
          :price="item.price"
          :imgUrl="item.imgUrl"
          @add-to-cart="handleAddToCart"
        />
      </div>
    </div>
    <!-- 購物車區 -->
    <div class="col-md-4">
      <h2 class="mb-3">購物車</h2>
      <ul class="list-group mb-3">
      <Cart v-for="item in cart" :key="item.id"
      :id="item.id"
      :title="item.title"
      :price="item.price"
      :count="item.count"
      @del-cart-item="handleDelItem"
      />
      </ul>
      <h3 class="text-end" v-if="sum > 0">總金額:{{sum}}</h3>
    </div>
    
  </div>

  <!-- 通知元件 -->
  <Notify v-if="message" @clear-msg="clearMessage"/>
</div>
  
</template>

<style scoped>
  body {
  background: #f2f2f2f2;
  }

.card-img-top {
  height: 150px;
  object-fit: cover;
}
</style>
