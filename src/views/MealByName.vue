<template>
    <div class="p-8 pb-0">
      <input type="text"
        v-model="keyword" 
        class="rounded border-2 border-grey-200 w-full"
        placeholder="Search For Meals"
        @change="searchMeals"
      />
    </div>
    <Meals :meals="meals" />
</template>

<script setup>
import {ref, computed, onMounted} from 'vue'
import axiosClient from '../axiosClient';
import store from '../store';
import {useRoute} from 'vue-router'
import Meals from '../components/Meals.vue'


const route = useRoute();
const keyword = ref("");
const meals = computed(() => store.state.searchedMeals);

function searchMeals() {
  if (keyword.value) {
    store.dispatch("searchMeals", keyword.value);
  } else {
    store.commit("setSearchedMeals", []);
  }
}

onMounted(() => {
  keyword.value = route.params.name
  if (keyword.value) {
    searchMeals()
  }
})
</script>