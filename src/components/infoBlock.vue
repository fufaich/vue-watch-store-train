<script setup>
const props = defineProps({
  imageUrl: String,
  description: String,
  title: String,
})
</script>

<template>
  <div class="flex-col flex gap-4 flex-1 items-center w-72 mx-auto">
    <div class="flex-1"></div>
    <img height="70" width="70" :src="imageUrl" alt="cart image"/>
    <h2 class="mt-4 text-2xl font-medium">{{title}}</h2>
    <p class="text-gray-400 text-center">{{description}}</p>
    <div class="flex-1"></div>
  </div>

</template>

<style scoped>

</style>