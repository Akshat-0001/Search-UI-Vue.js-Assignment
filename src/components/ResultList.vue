<script setup>
import ResultItem from './ResultItem.vue';

// Gets filtered list from app.vue and shows results
defineProps(['results']);
</script>

<template>
  <ul>
    <ResultItem v-for="(item, index) in results" :key="index" :item="item" />
  </ul>
</template>


<style>
ul {
  list-style: none;
  padding: 0;
  margin: 0;
  display: flex;
  flex-direction: column;
  gap: 10px;
}
</style>