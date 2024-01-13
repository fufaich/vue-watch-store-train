<script setup>

  const props = defineProps({
    id: Number,
    imageUrl: String,
    title: String,
    price: Number,
    isFavorite: Boolean,
    isAdded: {
      type: Boolean,
      default: false,
    },

    onClickFavorite: Function,
  })



</script>

<template>
  <div class="relative bg-white border border-slate-100 rounded-3xl p-8 cursor-pointer transition hover:-translate-y-2 hover:shadow-xl flex flex-col">
    <img :src="props.imageUrl" alt="Sneaker" class="scale-75 "/>
    <img :src="!props.isFavorite? '/like-1.svg' : '/like-2.svg'" alt="Plus" class="absolute top-8 left-8 transition scale-150" @click="onClickFavorite"/>

    <p class="mt-2">{{props.title}}</p>

    <div class="flex justify-between mt-5">
      <div class="flex flex-col">
        <span class="text-slate-500">Цена</span>
        <b>{{ props.price }} руб.</b>

      </div>
      <img :src="!isAdded? '/plus.svg' : '/checked.svg'" alt="Plus" @click="onClickAdd"/>

    </div>
  </div>
</template>

<style scoped>

</style>