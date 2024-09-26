<template>
  <div class="p-8 pb-0">
    <h1 class="text-4xl font-bold mb-4 text-orange-500">
      Meals for {{ ingredient.strIngredient }}
    </h1>
  </div>
  <Meals :meals="meals"></Meals>
</template>
<script setup>
import store from '../store';
import { computed, onMounted, ref } from 'vue';
import { useRoute } from 'vue-router';

import Meals from '../components/Meals.vue';

const meals = computed(() => store.state.mealsByIngredient);
const ingredient = computed(() => store.state.ingredient);
const route = useRoute();
onMounted(() => {
  store.dispatch('searchMealsByIngredient', route.params.ingredient);
});
</script>
