<script setup>
import { inject} from 'vue'

const emit = defineEmits(["showDrawer"]);
const cart = inject('cart');
const test = () => { console.log(cart.cart.value.sumCart) };
</script>

<template>
  <header class="flex justify-between border-b border-slate-200 py-8 px-10">
    <router-link to="/" class="cursor-pointer">
      <div class="flex items-center gap-4">
        <img
          src="/logo.png"
          alt="Logo"
          class="w-10"
          @click="test"
        />
        <div>
          <h2 class="font-bold text-xl uppercase">Vue Watch</h2>
          <p class="text-slate-400">Магазин лучших часов</p>
        </div>
      </div>
    </router-link>


    <ul class="flex items-center gap-5">
      <li class="flex items-center gap-3 text-gray-500 cursor-pointer hover:text-black" @click="emit('showDrawer')">
        <img src="/cart.svg" alt="Cart" />
        <b>{{ cart.cart.value.sumCart}} руб.</b>
      </li>
      <router-link to="/favorites">
        <li class="flex items-center gap-3 text-gray-500 cursor-pointer hover:text-black">
          <img src="/heart.svg" alt="Favorite"/>
          <span>Избранное</span>
        </li>
      </router-link>
      <li class="flex items-center gap-3 text-gray-500 cursor-pointer hover:text-black">
        <img src="/profile.svg" alt="Profile"/>
        <span>Профиль</span>
      </li>
    </ul>
  </header>
</template>

<style scoped>

</style>