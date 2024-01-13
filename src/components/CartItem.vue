<script setup>

  const props = defineProps({
    imageUrl: String,
    title: String,
    price: Number,
  })
  const emit = defineEmits(['clickDelete']);
</script>

<template>
  <div class="border border-slate-200 p-4 w-full rounded-xl flex gap-4 items-center">
    <img :src="props.imageUrl" alt="Sneaker" class="w-16 h-16">
    <div class="flex  flex-col">
      <p>{{props.title}}</p>
      <div class="flex justify-between mt-2">
        <b>{{props.price}} руб.</b>
        <img class= "opacity-40 hover:opacity-100 cursor-pointer transition"  src="/close.svg"  alt="Закрыть" @click="emit('clickDelete')"/>
      </div>
    </div>
  </div>
</template>

<style scoped>

</style>