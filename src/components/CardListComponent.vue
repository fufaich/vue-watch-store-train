<script setup>
import CardComponents from '@/components/CardComponents.vue'

defineProps({
  items: Array,
})
const onClickAdd = () => { alert('Добавить') };


</script>

<template>
  <div class="p-10">
    <div class="grid grid-cols-4 gap-5" >
      <CardComponents
        v-for="item in items"
        :key="item.id"

        :price="item.price"
        :title="item.title"
        :image-url="item.imageUrl"
        :onClickAdd="onClickAdd"
        :onClickFavorite="() => {}"
        :isFavorite="item.isFavorite"
      />

    </div>
  </div>
</template>
