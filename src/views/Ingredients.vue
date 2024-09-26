<template>
  <div class="p-8 pb-0">
    <h1 class="text-4xl font-bold mb-4 text-orange-500">Ingredients</h1>
  </div>
  <div class="px-8">
    <input
      type="text"
      class="rounded border-2 border-gray-200 w-full bg-white mb-3 focus:ring-orange-500 focus:border-orange-500"
      placeholder="Search for ingredients"
      v-model="keyword"
    />
    <div class="grid grid-cols-1 md:grid-cols-2 gap-3">
        <a href="#" @click.prevent="openIngredient(ingredient)" v-for="ingredient of computedIngredients" :key="ingredient.idIngredient" class="block bg-white rounded p-3 mb-3 shadow">
    
    <!-- <router-link
      :to="{
        name: 'byIngredient',
        params: { ingredient: ingredient.strIngredient },
      }"
      v-for="ingredient of computedIngredients"
      :key="ingredient.idIngredient"
      class="block bg-white rounded p-3 mb-3 shadow"
    > -->
      <h3 class="text-2xl font-bold" mb-2>{{ ingredient.strIngredient }}</h3>
    </a>
    </div>
      <!-- <p>{{ ingredient.strDescription }}</p>
    </router-link> -->
  </div>
</template>
<script setup>
import { onMounted, ref, computed } from 'vue';
import axiosClient from '../axiosClient';
import { useRouter } from 'vue-router';
import store from '../store';
const router = useRouter();
const keyword = ref("");
const ingredients = ref([]);
const computedIngredients = computed(() => {
  if (!computedIngredients) return ingredients;
  return ingredients.value.filter((i) =>
    i.strIngredient.toLowerCase().includes(keyword.value.toLowerCase())
  );
});

onMounted(() => {
  axiosClient.get('list.php?i=list').then(({ data }) => {
    ingredients.value = data.meals;
  });
});

function openIngredient(ingredient){
    store.commit('setIngredient', ingredient)
    router.push({
        name: "byIngredient",
        params:{ingredient:ingredient.strIngredient}
    })
}
</script>
