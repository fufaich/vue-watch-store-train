<script setup>

import CardListComponent from '@/components/CardListComponent.vue'
import { onMounted, ref } from 'vue'

const favorites = ref([]);

onMounted(() => {

})
</script>

<template>
<div class="flex flex-col gap-5 mb-4">
  <h2 class="text-2xl font-bold mb-5 flex-left">Избранное</h2>
  <CardListComponent items=""/>
</div>
</template>

<style scoped>

</style>