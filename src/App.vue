<script setup>
import { ref, computed, onMounted } from 'vue';
import SearchBar from './components/SearchBar.vue';
import ResultList from './components/ResultList.vue';
import Loader from './components/Loader.vue';

const searchQuery = ref('');
const loading = ref(false);
const isDark = ref(false);

const results = ref([]);

//  filters the results from search bar
const filteredResults = computed(() => {
  return results.value.filter(item => item.title.toLowerCase().includes(searchQuery.value.toLowerCase()));
});

// debounce
let timeout;

const handleSearch = (value) => {
  clearTimeout(timeout);
  timeout = setTimeout(() => { searchQuery.value = value; }, 300); };

const ChangeTheme = () => {isDark.value = !isDark.value;};

onMounted(async () => {
  //  fetching data ffrom api and mapping it to our usecase
  loading.value = true;
  try {
    const response = await fetch('https://dummyjson.com/products?limit=22');
    const data = await response.json();
    results.value = data.products.map(item => ({
      title: item.title,
      snippet: item.description
    }));
  } catch (error) {
    console.error('Failed to fetch results:', error);
  } finally {
    loading.value = false;
  }
  });

</script>


<template>

<div :class="['page', isDark ? 'dark' : 'light']">
  <div class="container">
    <button class="theme-toggle" @click="ChangeTheme">Change Theme</button>
    <SearchBar @updateSearch="handleSearch"/>
    <Loader v-if="loading" />
    <p v-else-if="filteredResults.length === 0"> No results found </p>
    <ResultList v-else :results="filteredResults" />
  </div>
</div>

</template>


<style>
*,
*::before,
*::after {
  box-sizing: border-box;
}

body {
  font-family: Arial, sans-serif;
  margin: 0;
}

.page {
  min-height: 100vh;
  padding: 40px 0;
  transition: background-color 0.2s ease, color 0.2s ease;
}

.container {
  max-width: 600px;
  margin: 0 auto;
  padding: 16px;
  border-radius: 10px;
  transition: background-color 0.2s ease, color 0.2s ease;
  overflow-x: hidden;
}

.light {
  --card-bg: #ffffff;
  --text-color: #111827;
  --muted-text: #6b7280;
  --border-color: #d1d5db;
  --input-bg: #ffffff;
  --hover-bg: #f3f4f6;
  --button-bg: #e5e7eb;
  --button-text: #111827;
  --accent: #4f46e5;
  background: #e5e7eb;
  color: #111827;
}

.dark {
  --card-bg: #374151;
  --text-color: #f9fafb;
  --muted-text: #d1d5db;
  --border-color: #4b5563;
  --input-bg: #374151;
  --hover-bg: #4b5563;
  --button-bg: #4b5563;
  --button-text: #f9fafb;
  --accent: #818cf8;
  background: #111827;
  color: #f9fafb;
}

.theme-toggle {
  margin-bottom: 15px;
  padding: 6px 10px;
  border: 1px solid var(--border-color);
  border-radius: 6px;
  background: var(--button-bg);
  color: var(--button-text);
  cursor: pointer;
}
</style>