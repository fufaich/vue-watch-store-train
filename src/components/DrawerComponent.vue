<script setup>

import DrawerHeadComponent from '@/components/DrawerHeadComponent.vue'
import CartListItem from '@/components/CartListItem.vue'
import { computed, inject } from 'vue'
import InfoBlock from '@/components/infoBlock.vue'
const cart = inject('cart')
const props = defineProps({
  isCreatingOrder: Boolean,
})

const buttonDisabled = computed(() => props.isCreatingOrder.value ? true: cart.cart.value.sumCart? false: true);
</script>

<template>
  <div class="fixed top-0 left-0 h-full w-full bg-black z-10 opacity-70" @click="cart.changeDrawer()"></div>
  <div class="bg-white w-96 h-full fixed top-0 right-0 z-20 p-8 flex flex-col">
    <DrawerHeadComponent/>

    <InfoBlock
      v-if="cart.cart.value.cartList.length === 0"
     title="Корзина пустая"
     description="Добавьте хотя бы одну пару кроссовок, чтобы сделать заказ."
     image-url="/package-icon.png"
     class=""
    />
    <CartListItem
     v-else
    />

    <div class="flex flex-col gap-4  mt-7" v-if="cart.cart.value.cartList.length !== 0">
      <div class="flex gap-2">
        <span>Итого: </span>
        <div class="flex-1 border-b border-dashed"></div>
        <b>{{cart.cart.value.sumCart}} р.</b>
      </div>
      <div class="flex gap-2">
        <span>Налог: </span>
        <div class="flex-1 border-b border-dashed"></div>
        <b>{{cart.cart.value.sumCart/ 100 * 5}} р.</b>
      </div>
      <button
        class="bg-lime-500 text-white p-2 rounded-xl w-full py-3 disabled:bg-slate-300 hover:bg-lime-600 hover:shadow-xl transition cursor-pointer"
        @click="cart.createOrder"
        :disabled="buttonDisabled"
      >Оформить заказ</button>

    </div>
  </div>
</template>

<style scoped>

</style>