<script setup>
import { onMounted, ref, watch } from 'vue'
import HeaderComponent from '@/components/HeaderComponent.vue'
import CardListComponent from '@/components/CardListComponent.vue'
import DrawerComponent from '@/components/DrawerComponent.vue'
import axios from 'axios'

const items = ref([]);

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

const fetchItems = async () =>{
    try {
      const params ={
        sortBy: filters.value.sortBy,
      }

      if(filters.value.searchQuery){
        params.title = `*${filters.value.searchQuery}*`
      }
      const { data } = await axios.get(`https://604781a0efa572c1.mokky.dev/items`,
        {
          params
        });

      items.value = data.map(obj => ({...obj, isFavorite: false, isAdded: false}));
    }catch (e) {
      console.log(e)
    }
}

const fetchFavorites = async () =>
{
  try {
    const {data: favorites} = await axios.get(`https://604781a0efa572c1.mokky.dev/favorites`);
    console.log(favorites);
    favorites.map(favorite =>{
      // console.log(favorite);
      items.value = items.value.map(item => {
        if(item.id === favorite.itemId){
          return {...item, isFavorite: true};
        }else{
          return {...item};
        }
      })
    })
    console.log(items.value);
  } catch (e) {
    console.log(e);
  }
};

onMounted(async () =>{
  await fetchItems();
  await fetchFavorites()
});
watch(filters, ()=>{
  fetchItems();
  fetchFavorites();
},  {deep: true});
</script>

<template>
  <div class="bg-white w-4/5 m-auto rounded-xl shadow-xl mt-14 ">
    <HeaderComponent />
    <div class="p-10">
      <div class="flex justify-between items-center">
        <h2 class="text-3xl font-bold mb-5">Все кроссовки</h2>
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
    <CardListComponent :items="items"/>
<!--    <DrawerComponent/>-->




  </div>
</template>

