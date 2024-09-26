<template>
  <div class="p-8 pb-0">
    <h1 class="text-4xl font-bold mb-4 text-orange-500">Search Meals by Name</h1>
  </div>
  <div class="p-8 pb-3">
    <input
      type="text"
      class="rounded border-2 border-gray-200 w-full bg-white focus:ring-orange-500 focus:border-orange-500"
      placeholder="Search for meals"
      v-model="keyword"
      @change="searchMeals"
    />
  </div>
  <Meals :meals="meals"></Meals>
</template>
<script setup>
import { ref, computed, onMounted } from 'vue';
import { useRoute } from 'vue-router';
import store from '../store';
import Meals from '../components/Meals.vue';

const keyword = ref('');
const meals = computed(() => store.state.searchedMeals);
const route = useRoute();
function searchMeals() {
  if (keyword.value) {
    store.dispatch('searchMeals', keyword.value);
  } else {
    store.commit('setSearchedMeals', []);
  }
}
onMounted(() => {
  keyword.value = route.params.name;
  if (keyword.value) {
    searchMeals();
  }
});
</script>
