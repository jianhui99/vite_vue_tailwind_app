<template>
  <div class="p-8">
    <h1 class="text-4xl font-bold mb-4 text-red-500">Ingredients</h1>
  </div>

  <div class="p-8">
    <input 
      type="text"
      class="rounded border-2 border-gray-200 w-full" 
      placeholder="Search for Ingredients"
      v-model="keyword"
      @change="searchIngredients"
    />
  </div>

  <div class="p-8">
    <router-link 
      :to="{name:'byIngredient', params:{ingredient:ingredient.strIngredient}}" 
      v-for="ingredient of computedIngredients" 
      :key="ingredient.idIngredient" 
      class="block bg-white rounded-xl p-3 mb-3 shadow hover:bg-red-400 hover:text-white transition-all duration-500"
      >
      <h2 class="text-2xl font-bold mb-2">{{ingredient.strIngredient}}</h2>
      <p>{{ingredient.strDescription}}</p>
    </router-link>
  </div>
</template>

<script setup>
import {computed, onMounted, ref} from 'vue'
import {useRoute} from 'vue-router'
import store from "../store";
import axiosClient from '../axiosClient';

const ingredients = ref([])
const keyword = ref('')

const computedIngredients = computed(() => {
  return ingredients.value.filter(ingredient => {
    return ingredient.strIngredient.toLowerCase().includes(keyword.value.toLowerCase())
  })
});

onMounted(() => {
  axiosClient.get('list.php?i=list')
    .then(res => {
      ingredients.value = res.data.meals
    })
})

</script>