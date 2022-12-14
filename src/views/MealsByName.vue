<template>
  <div class="p-8 pb-0 ">
    <input v-model="keyword" type="text" class="rounded border-2 bg-white border-gray-200 w-full focus:ring-orange-500"
      placeholder="Search for Meals" @change="searchMeals">
  </div>

  <Meals :meals="meals" />
</template>


<script setup>
import { computed } from "@vue/reactivity";
import { ref } from "vue";
import { onMounted } from "vue"
import { useRoute } from "vue-router";
import Meals from "../components/Meals.vue";
import store from "../store";

const route = useRoute();
const keyword = ref("");
const meals = computed(() => store.state.searchedMeals);

function searchMeals() {
  if (keyword.value) {
    store.dispatch('searchMeals', keyword.value)
  } else {
    store.commit('setSearchedMeals', []);
  }
}

onMounted(() => {
  keyword.value = route.params.name
  if (keyword.value) {
    searchMeals
  }
})

</script>