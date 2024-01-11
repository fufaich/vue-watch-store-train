<script setup>
  defineProps({
    imageUrl: String,
    title: String,
    price: Number,
  })
</script>

<template>
  <div class="border border-slate-200 p-4 w-full rounded-xl flex gap-4 items-center">
    <img :src="imageUrl" alt="Sneaker" class="w-16 h-16">
    <div class="flex  flex-col">
      <p>Кроссовки Nike air max 123</p>
      <div class="flex justify-between mt-2">
        <b>12 999р.</b>
        <img class= "opacity-40 hover:opacity-100 cursor-pointer transition"  src="/close.svg" />
      </div>
    </div>
  </div>
</template>

<style scoped>

</style>