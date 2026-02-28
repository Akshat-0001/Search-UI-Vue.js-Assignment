<script setup>
// sends input value to app.vue so that filtering happens there
const emit = defineEmits(['updateSearch']);

</script>

<template>
  <input class="search-input" type="text" placeholder="Search..." @input="emit('updateSearch', $event.target.value)" />
</template>


<style scoped>
.search-input {
  display: block;
  width: 100%;
  max-width: 100%;
  min-width: 0;
  padding: 10px 12px;
  border: 1px solid var(--border-color);
  border-radius: 6px;
  font-size: 14px;
  margin-bottom: 20px;
  background: var(--input-bg);
  color: var(--text-color);
}

.search-input::placeholder {
  color: var(--muted-text);
}

.search-input:focus {
  outline: none;
  border-color: var(--accent);
}
</style>