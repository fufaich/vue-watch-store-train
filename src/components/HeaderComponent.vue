<script setup>
import { inject, onMounted, ref, watch } from 'vue'

const emit = defineEmits(["showDrawer"]);
const cart = inject('cart');
const test = () => { console.log(cart.cart.value.sumCart) };
</script>

<template>
  <header class="flex justify-between border-b border-slate-200 py-8 px-10">

    <div class="flex items-center gap-4">
      <img src="/logo.png" alt="Logo" class="w-10" @click="test"/>
      <div>
        <h2 class="font-bold text-xl uppercase">Vue Watch</h2>
        <p class="text-slate-400">Магазин лучших часов</p>
      </div>
    </div>

    <ul class="flex items-center gap-5">
      <li class="flex items-center gap-3 text-gray-500 cursor-pointer hover:text-black" @click="emit('showDrawer')">
        <img src="/cart.svg" alt="Cart" />
        <b>{{ cart.cart.value.sumCart}} руб.</b>
      </li>
      <li class="flex items-center gap-3 text-gray-500 cursor-pointer hover:text-black">
        <img src="/heart.svg" alt="Favorite"/>
        <span>Избранное</span>
      </li>
      <li class="flex items-center gap-3 text-gray-500 cursor-pointer hover:text-black">
        <img src="/profile.svg" alt="Profile"/>
        <span>Профиль</span>
      </li>
    </ul>
  </header>
</template>

<style scoped>

</style>