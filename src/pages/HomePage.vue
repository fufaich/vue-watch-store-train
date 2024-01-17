<script setup>

import CardListComponent from '@/components/CardListComponent.vue'
import axios from 'axios'
import { inject, onMounted, ref, watch } from 'vue'

const cart = inject('cart')

const filters = ref({
  sortBy: 'title',
  searchQuery: '',
});

const onChangeSelect = (event) => {
  filters.value.sortBy = event.target.value;
};

const onChangeSearch = (event) => {
  filters.value.searchQuery= event.target.value;
};

const addToCart = (item) =>{
  if(!item.isAdded){
    cart.cart.value.cartList.push(item)
    item.isAdded = true;
  }else{
    cart.cart.value.cartList.splice(cart.cart.value.cartList.indexOf(item),1);
    item.isAdded = false;
  }
}

const addToFavorite = async (item) =>{
  try{
    if (!item.isFavorite) {
      item.isFavorite = true;
      const obj = {
        itemId: item.id,
      }
      const {data} = await axios.post(`https://78f600b7e2539b8d.mokky.dev/favorites`, obj);
      item.favoriteId = data.id
    }else {
      item.isFavorite = false;
      await axios.delete(`https://78f600b7e2539b8d.mokky.dev/favorites/${item.favoriteId}`);
      item.favoriteId = null;
    }
  }catch (e) {
    console.log(e);
  }
}

const fetchItems = async () =>{
  try {
    const params ={
      sortBy: filters.value.sortBy,
    }

    if(filters.value.searchQuery){
      params.title = `*${filters.value.searchQuery}*`
    }
    const { data } = await axios.get(`https://78f600b7e2539b8d.mokky.dev/items`,
      {
        params
      });

    cart.items.value = data.map(obj => ({...obj, isFavorite: false, isAdded: false, favoriteId: null}));
  }catch (e) {
    console.log(e)
  }
}
const fetchFavorites = async () =>
{
  try {
    const {data: favorites} = await axios.get(`https://78f600b7e2539b8d.mokky.dev/favorites`);
    favorites.map(favorite =>{

      cart.items.value = cart.items.value.map(item => {
        if(item.id === favorite.itemId){
          return {...item, isFavorite: true, favoriteId: favorite.id};
        }else{
          return {...item};
        }
      })
    })
  } catch (e) {
    console.log(e);
  }
};

watch(filters, ()=>{
  fetchItems();
  fetchFavorites();
},  {deep: true});

onMounted(async () =>{

  await fetchItems();
  await fetchFavorites();

});

</script>

<template>
  <div class="flex justify-between items-center">
    <h2 class="text-3xl font-bold mb-5">Все часы</h2>
    <div class="flex gap-4">
      <select class="py-2 px-4 border border-gray-300 rounded-lg" @change="onChangeSelect">
        <option value="name">По названию</option>
        <option value="price">По цене (дешевые)</option>
        <option value="-price">По цене (дорогие)</option>
      </select>
      <div class="relative">
        <img src="/search.svg" alt="" class="absolute left-3 top-3">
        <input
          placeholder="Поиск..."
          class="border border-gray-300 py-2 pl-11 pr-4 outline-none rounded-lg focus:border-gray-400"
          @input="onChangeSearch"
        />
      </div>
    </div>
  </div>
  <CardListComponent :items="cart.items.value" @addToFavorite="addToFavorite" @addToCart="addToCart"/>
</template>

<style scoped>

</style>