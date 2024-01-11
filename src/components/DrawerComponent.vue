<script setup>

import DrawerHeadComponent from '@/components/DrawerHeadComponent.vue'
import CartListItem from '@/components/CartListItem.vue'
</script>

<template>
  <div class="fixed top-0 left-0 h-full w-full bg-black z-10 opacity-70"></div>
  <div class="bg-white w-96 h-full fixed top-0 right-0 z-20 p-8 flex flex-col">
    <DrawerHeadComponent/>
    <CartListItem/>

    <div class="flex flex-col gap-4  mt-7">
      <div class="flex gap-2">
        <span>Итого: </span>
        <div class="flex-1 border-b border-dashed"></div>
        <b>12900 р.</b>
      </div>
      <div class="flex gap-2">
        <span>Налог: </span>
        <div class="flex-1 border-b border-dashed"></div>
        <b>900 р.</b>
      </div>
      <button class="bg-lime-500 text-white p-2 rounded-xl w-full py-3 disabled:bg-slate-300 hover:bg-lime-600 hover:shadow-xl transition cursor-pointer" disabled="">Оформить заказ</button>

    </div>
  </div>
</template>

<style scoped>

</style>