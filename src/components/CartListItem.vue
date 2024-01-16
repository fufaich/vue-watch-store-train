<script setup>
import { inject } from 'vue'
import CartItem from '@/components/CartItem.vue'

const cart = inject("cart");

</script>

<template>
    <div class="flex-col flex gap-4 flex-1" v-auto-animate >
      <CartItem v-for="item in cart.cart.value.cartList" :key="item.id"
        :image-url="item.imageUrl"
        :title="item.title"
        :price="item.price"
                @clickDelete="() =>{
                  cart.addToCart(item);
                  console.log(item);
                }"
      />

    </div>
</template>

<style scoped>

</style>