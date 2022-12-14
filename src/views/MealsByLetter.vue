<template>
  <div class="flex justify-center gap-2 mt-2">
    <router-link :to="{ name: 'byLetter', params: { letter } }" v-for="letter of letters">
      {{ letter }}
    </router-link>
  </div>

  <div>
    <pre>{{ meals }}</pre>
  </div>
</template>


<script setup>
import { computed } from '@vue/reactivity';
import store from '../store';

const letters = "ABCDEFGHIJKLMNOPQRSTUVWXYZ".split("");
const meals = computed(() => store.state.mealsByLetter)
</script>