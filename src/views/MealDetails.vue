<template>
  <div class="w-[800px] mx-auto p-8" v-if="meal.idMeal">
    <h1 class="text-5xl font-bold mb-5">{{meal.strMeal}}</h1>
    <img :src="meal.strMealThumb" :alt="meal.strMeal">
    <div class="grid grid-cols-1 sm:grid-cols-3 text-lg py-2">
        <div>
            <strong class="font-bold"> Category: </strong> {{meal.strCategory}}
        </div>
        <div>
            <strong class="font-bold"> Area: </strong>  {{meal.strArea}}
        </div>
        <div>
            <strong class="font-bold"> Tags: </strong>  {{meal.strTags}}
        </div>
    </div>

    <div class="my-3">
        {{meal.strInstructions}}
    </div>

    <div class="grid grid-cols-1 md:grid-cols-2">
        <div>
            <h2 class="text-2xl font-semibold mb3">Ingredients</h2>
            <ul>
                <template v-for="(el, ind) of new Array(20)">
                    <li v-if="meal[`strIngredient${ind+1}`]">
                       {{ind+1}}. {{meal[`strIngredient${ind+1}`]}}
                    </li>
                </template>
            </ul>
        </div>

        <div>
            <h2 class="text-2xl font-semibold mb3">Measures</h2>
            <ul>
                <template v-for="(el, ind) of new Array(20)">
                    <li v-if="meal[`strMeasure${ind+1}`]">
                       {{ind+1}}. {{meal[`strMeasure${ind+1}`]}}
                    </li>
                </template>
            </ul>
        </div>

        <div class="mt-5">
          <YouTubeButton :href="meal.strYoutube">Go To YouTube </YouTubeButton>
          <a
          :href="meal.strSource"
          target="_blank"
          class="ml-3 px-3 py-2 rounded border-2 border-transparent text-indigo-600 transition-colors"
        >
          View Original Source
        </a>
        </div>
    </div>
  </div>

  <div v-else>
    <h1>Opps! somethings went wrong, pleasae try again later.</h1>
  </div>
</template>

<script setup>
import {computed, onMounted, ref} from 'vue'
import {useRoute} from 'vue-router'
import axiosClient from '../axiosClient';
import YouTubeButton from '../components/YouTubeButton.vue'

const route = useRoute()
const meal = ref({})

onMounted(() => {
    axiosClient.get(`lookup.php?i=${route.params.id}`)
        .then(res => {
            meal.value = res.data.meals[0]
        })
        .catch(err => {
            console.log(err)
        })
})
</script>

<style>

</style>