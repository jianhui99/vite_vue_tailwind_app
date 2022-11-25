<template>
  <header class="bg-white shadow h-16 flex justify-between items-stretch">
      <router-link :to="{name:'home'}" class="inline-flex items-center h-full px-5">Home</router-link>
      <div class="flex items-center gap-1">
        <router-link :to="{name:'byName'}" class="px-2 h-full hover:bg-purple-100 inline-flex items-center transition-colors">
          Meals
        </router-link>
        <router-link :to="{name:'byLetter'}" class="px-2 h-full hover:bg-purple-100 inline-flex items-center transition-colors">
          Meals By Letter
        </router-link>
        <router-link :to="{name:'ingredients'}" class="px-2 h-full hover:bg-purple-100 inline-flex items-center transition-colors">
          Ingredients
        </router-link>
      </div>
    </header>
</template>