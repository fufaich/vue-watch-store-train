<script setup>
import CardComponents from '@/components/CardComponents.vue'
const onClickAdd = () => { alert('Добавить') };
const onClickFavorite = () => { alert('Лайкнуть') };

</script>

<template>
  <div class="p-10">
    <h2 class="text-3xl font-bold mb-5">Все кроссовки</h2>
    <div class="grid grid-cols-4 gap-5">
      <CardComponents
        :price="5000"
        title="Мужские Кроссовки Nike Blazer Mid Suede"
        image-url="/sneakers/sneakers-1.jpg"
        is-favorite
        is-added
        :onClickAdd="onClickAdd"
        :onClickFavorite="onClickFavorite"
      />

    </div>
  </div>
</template>
