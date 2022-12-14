<template>
  <Meals :meals="meals" />
</template>


<script setup>
import Meals from "../components/Meals.vue"
import { computed } from "@vue/reactivity"
import { onMounted, ref } from 'vue';
import { useRoute } from "vue-router";
import store from '../store';

const route = useRoute();
const meals = computed(() => store.state.mealsByIngredient)

onMounted(() => {
  store.dispatch('searchMealsByIngredient', route.params.ingredient)
})

</script>