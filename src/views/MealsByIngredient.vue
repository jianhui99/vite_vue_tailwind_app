<template>
  <div class="p-8">
    <h1 class="text-4xl font-bold mb-4 text-red-500">Meals By Ingredients</h1>
  </div>

  <div class="grid grid-cols-1 md:grid-cols-3 gap-5 p-8" v-if="meals">
      <MealItem  v-for="meal of meals" :key="meal.idMeal" :meal="meal"/>
    </div>
</template>

<script setup>
import {computed, onMounted, ref} from 'vue'
import {useRoute} from 'vue-router'
import store from "../store";
import axiosClient from '../axiosClient';
import MealItem from '../components/MealItem.vue'

const meals = computed(() => store.state.mealsByIngredient);
const route = useRoute()

onMounted(()=>{
  store.dispatch("searchMealsByIngredient", route.params.ingredient);
})



</script>