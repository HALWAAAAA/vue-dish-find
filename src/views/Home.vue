<template>
  <div class="text-orange-500 p-8 pb-0">
    <h1 class="text-4xl font-bold mb-4">Random meals</h1>
  </div>
  <Meals :meals="meals"></Meals>
</template>
<script setup>
import { computed, onMounted, ref } from 'vue';
import store from '../store';
import axiosClient from '../axiosClient';
import Meals from '../components/Meals.vue';
const meals = ref([]);

onMounted(async () => {
  for (let i = 0; i < 12; i++) {
    axiosClient
      .get(`random.php`)
      .then(({ data }) => meals.value.push(data.meals[0]));
  }
});
</script>
