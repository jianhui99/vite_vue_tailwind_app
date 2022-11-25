<template>
  <div class="p-8">
    <h1 class="text-4xl font-bold mb-4 text-red-500">Meals</h1>
  </div>
  <div class="p-8">
    <input 
      type="text"
      class="rounded border-2 border-gray-200 w-full" 
      placeholder="Search for Meals"
      v-model="keyword"
      @change="searchMeals"
    />
  </div>

  <div class="grid grid-cols-1 md:grid-cols-3 gap-5 p-8">
    <MealItem  v-for="meal of meals" :key="meal.idMeal" :meal="meal"/>
  </div>

  <div v-if="!meals">
    <p class="text-center text-2xl">No meals found</p>
  </div>
</template>

<script setup>
import {computed, onMounted, ref} from 'vue'
import {useRoute} from 'vue-router'
import store from "../store";
import MealItem from '../components/MealItem.vue'

const keyword = ref('')
const route = useRoute()
const meals = computed(() => store.state.searchedMeals);

function searchMeals(){
  if(keyword.value){
    store.dispatch("searchMeals", keyword.value);
  }else{
    store.commit("setSearchedMeals", []);
  }
}

onMounted(() => {
  keyword.value = route.params.name
  if(keyword.value){
    searchMeals()
  }
})

</script>

<style>

</style>