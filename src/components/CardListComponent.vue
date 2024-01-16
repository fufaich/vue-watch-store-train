<script setup>
import CardComponents from '@/components/CardComponents.vue'

defineProps({
  items: Array,
})

const emit = defineEmits(['addToFavorite','addToCart']);

</script>

<template>
  <div class="p-10">
    <div class="grid grid-cols-4 gap-5" v-auto-animate >
      <CardComponents
        v-for="item in items"
        :key="item.id"
        :id="item.id"
        :price="item.price"
        :title="item.title"
        :image-url="item.imageUrl"
        :onClickAdd="() => emit('addToCart', item)"
        :onClickFavorite="() => emit('addToFavorite', item) "
        :isFavorite="item.isFavorite"
        :isAdded = "item.isAdded"
      />
    </div>
  </div>
</template>
