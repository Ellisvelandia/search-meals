<template>
  <div class="flex justify-center gap-2 mt-2">
    <router-link :to="{ name: 'byLetter', params: { letter } }" v-for="letter of letters">
      {{ letter }}
    </router-link>
  </div>

  <Meals :meals="meals" />
</template>


<script setup>
import { computed } from '@vue/reactivity';
import { onMounted, watch } from 'vue';
import { useRoute } from 'vue-router';
import Meals from '../components/Meals.vue';
import store from '../store';

const route = useRoute()
const letters = "ABCDEFGHIJKLMNOPQRSTUVWXYZ".split("");
const meals = computed(() => store.state.mealsByLetter)

watch(route, () => {
  store.dispatch('searchMealsByLetter', route.params.letter)
})

onMounted(() => {
  store.dispatch('searchMealsByLetter', route.params.letter)
})

</script>