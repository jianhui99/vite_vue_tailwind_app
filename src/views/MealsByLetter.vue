<template>
    <div class="p-8 pb-0">
      <h1 class="text-4xl font-bold mb-4 text-red-500">Meals by Letter</h1>
    </div>

    <div class="flex flex-wrap justify-center gap-5 p-8 mb-6">
      <router-link 
        v-for="letter of letters" 
        :to="{name: 'byLetter', params:{letter}}" 
        class="w-2 h-2 flex items-center justify-center hover:text-red-500 hover:scale-150 hover:font-bold transition-all">
        {{ letter }}
      </router-link>
    </div>

    <div class="grid grid-cols-1 md:grid-cols-3 gap-5 p-8" v-if="meals.length">
      <MealItem  v-for="meal of meals" :key="meal.idMeal" :meal="meal"/>
    </div>

    <div v-else>
      <div v-if="letter">
        <p class="text-center text-2xl">No meals found</p>
      </div>
    </div>
    
</template>

<script setup>
import {computed, onMounted, ref, watch} from 'vue'
import {useRoute} from 'vue-router'
import store from "../store";
import MealItem from '../components/MealItem.vue'

const letters = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ'.split("");
const letter = ref('')
const route = useRoute()
const meals = computed(() => store.state.mealsByLetter);

watch(route, ()=>{
  store.dispatch("searchMealsByLetter", route.params.letter);
  letter.value = route.params.letter;
})
</script>
