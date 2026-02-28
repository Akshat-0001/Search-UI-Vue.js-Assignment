<script setup>
import { ref } from 'vue';

defineProps(['item']);

// check if item is expanded or not
const isExpanded = ref(false);

// closes/opens item when clicked
const clicked = () => {
  isExpanded.value = !isExpanded.value; };
</script>

<template>
  <li @click="clicked">
    <h3>{{ item.title }}</h3>

    <transition name="fade">
      <p v-if="isExpanded">
        {{ item.snippet }}
      </p>
    </transition>
  </li>
</template>


<style>
.fade-enter-active,
.fade-leave-active { transition: opacity 0.3s; }

.fade-enter-from,
.fade-leave-to { opacity: 0; }

li {
  background: var(--card-bg);
  padding: 12px 15px;
  border-radius: 8px;
  border: 1px solid var(--border-color);
  transition: all 0.2s ease;
  cursor: pointer;
}

li:hover { background: var(--hover-bg); }

h3 {
  margin: 0;
  font-size: 16px;
  color: var(--text-color);
}

p {
  margin-top: 8px;
  font-size: 14px;
  color: var(--muted-text);
}
</style>