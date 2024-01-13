<script setup>
import { inject } from 'vue'
import CartItem from '@/components/CartItem.vue'

const cart = inject("cart");

</script>

<template>
    <div class="flex-col flex gap-4 flex-1" >
      <CartItem v-for="item in cart.cartList.value" :key="item.id"
        :image-url="item.imageUrl"
        :title="item.title"
        :price="item.price"
      />

    </div>
</template>

<style scoped>

</style>