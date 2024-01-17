<script setup>
import { provide, ref, watch } from 'vue'
import HeaderComponent from '@/components/HeaderComponent.vue'
import DrawerComponent from '@/components/DrawerComponent.vue'
import axios from 'axios'
import HomePage from '@/pages/HomePage.vue'

const cart = ref({
  cartList: [],
  sumCart: 0,
});
const items = ref([]);
const drawerOpen = ref(false); // DrawerOpen

const isCreatingOrder = ref(false);


const createOrder = async () => {
  try {
    isCreatingOrder.value = true;
    const obj = {
      items: cart.value.cartList,
      total: cart.value.sumCart
    }
    await axios.post('https://78f600b7e2539b8d.mokky.dev/orders', obj);
    cart.value.cartList = [];
    cart.value.sumCart = 0;
    items.value = items.value.map(obj => ({...obj,  isAdded: false}));
    // changeDrawer();
  }catch (e){
    console.log(e);
  }finally {
    isCreatingOrder.value = false;
  }
}

const addToCart = (item) =>{
  if(!item.isAdded){
    cart.value.cartList.push(item)
    item.isAdded = true;
  }else{
    cart.value.cartList.splice(cart.value.cartList.indexOf(item),1);
    item.isAdded = false;
  }
}

const changeDrawer = () =>{
  drawerOpen.value = !drawerOpen.value;
}



watch(cart.value.cartList, async ()=>{
  cart.value.sumCart = cart.value.cartList.reduce((acc, item) => acc + item.price, 0);
  localStorage.setItem('cart', JSON.stringify(cart.value));
})
provide('cart', {
  changeDrawer,
  createOrder,
  addToCart,
  items,
  cart: cart,
});
</script>

<template>
  <div class="bg-white w-4/5 m-auto rounded-xl shadow-xl mt-14 ">
    <HeaderComponent  @showDrawer = 'changeDrawer'/>
    <div class="p-10">
      <router-view></router-view>
    </div>
    <DrawerComponent v-if="drawerOpen" :isCreatingOrder="isCreatingOrder"/>




  </div>
</template>

