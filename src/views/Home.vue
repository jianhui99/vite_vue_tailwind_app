<template>
  <div class="p-8">
    <h1 class="text-4xl font-bold mb-4 text-red-500">Welcome to Meals Search App</h1>
  </div>
</template>

<script setup>
  import { computed, onMounted, ref } from 'vue';
  import store from '../store';
  import axiosClient from '../axiosClient';

  const letters = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ'.split("");
  const ingredients = ref([])

  onMounted(async() => {
    const res = await axiosClient.get('/list.php?i=list');
    ingredients.value = res.data;
  });
</script>

<style>

</style>