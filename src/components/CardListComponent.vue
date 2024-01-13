<script setup>
import CardComponents from '@/components/CardComponents.vue'

defineProps({
  items: Array,
})
const onClickAdd = () => { alert('Добавить') };

const emit = defineEmits(['addToFavorite']);

</script>

<template>
  <div class="p-10">
    <div class="grid grid-cols-4 gap-5" >
      <CardComponents
        v-for="item in items"
        :key="item.id"
        :id="item.id"
        :price="item.price"
        :title="item.title"
        :image-url="item.imageUrl"
        :onClickAdd="onClickAdd"
        :onClickFavorite="() => emit('addToFavorite', item)"
        :isFavorite="item.isFavorite"
      />
    </div>
  </div>
</template>
