<template>
  <div class="p-8 pb-0">
    <h1 class="text-4xl font-bold mb-4 text-orange-500">Ingredients</h1>
    <div class="px-8">

      <input v-model="keyword" type="text" class="rounded border-2 bg-white border-gray-200  w-full mb-3 focus:ring-orange-500"
        placeholder="Search for Ingredients">

      <router-link :to="{ name: 'byIngredient', params: { ingredient: ingredient.strIngredient } }"
        v-for="ingredient of computedIngredients" :key="ingredient.idIngredient"
        class="block  bg-white rounded p-3 mb-3 shadow">
        <h3 class="text-2xl font-bold mb-2">
          {{ ingredient.strIngredient }}
        </h3>
        <p>{{ ingredient.strDescription }}</p>
      </router-link>
    </div>
  </div>
</template>


<script setup>
import { computed } from '@vue/reactivity';
import { onMounted, ref } from 'vue';
import axiosClient from '../axiosClient';

const keyword = ref('');
const ingredients = ref([]);
const computedIngredients = computed(() => {
  if (!computedIngredients) return ingredients;
  return ingredients.value.filter((i) => i.strIngredient.toLowerCase().includes(keyword.value.toLowerCase()));
});

onMounted(() => {
  axiosClient.get('list.php?i=list')
    .then(({ data }) => {
      ingredients.value = data.meals;
    })
})

</script>