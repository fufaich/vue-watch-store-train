<script setup>
import { onMounted, provide, ref, watch } from 'vue'
import HeaderComponent from '@/components/HeaderComponent.vue'
import CardListComponent from '@/components/CardListComponent.vue'
import DrawerComponent from '@/components/DrawerComponent.vue'
import axios from 'axios'

const items = ref([]);
const cart = ref([]);
const drawerOpen = ref(false); // DrawerOpen
const filters = ref({
  sortBy: 'title',
  searchQuery: '',
});

const addToCart = (item) =>{
  if(!item.isAdded){
    cart.value.push(item);
    item.isAdded = true;
  }else{
    cart.value.splice(cart.value.indexOf(item),1);
    item.isAdded = false;
  }
}





const changeDrawer = () =>{
  drawerOpen.value = !drawerOpen.value;
}
const onChangeSelect = (event) => {
  filters.value.sortBy = event.target.value;
};

const onChangeSearch = (event) => {
  filters.value.searchQuery= event.target.value;
};

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

      items.value = data.map(obj => ({...obj, isFavorite: false, isAdded: false, favoriteId: null}));
    }catch (e) {
      console.log(e)
    }
}
const fetchFavorites = async () =>
{
  try {
    const {data: favorites} = await axios.get(`https://78f600b7e2539b8d.mokky.dev/favorites`);
    favorites.map(favorite =>{

      items.value = items.value.map(item => {
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

onMounted(async () =>{
  await fetchItems();
  await fetchFavorites()
});
watch(filters, ()=>{
  fetchItems();
  fetchFavorites();
},  {deep: true});

provide('cart', {
  changeDrawer,
  cartList: cart,
});
</script>

<template>
  <div class="bg-white w-4/5 m-auto rounded-xl shadow-xl mt-14 ">
    <HeaderComponent  @showDrawer = 'changeDrawer'/>
    <div class="p-10">
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
    </div>
    <CardListComponent :items="items" @addToFavorite="addToFavorite" @addToCart="addToCart"/>
    <DrawerComponent v-if="drawerOpen" />



  </div>
</template>

