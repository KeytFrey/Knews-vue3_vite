<script setup lang="ts">
import NewsView from './View/NewsView.vue';
</script>

<template>
  <NewsView />
</template>

<style>
body {
  margin: 0;
  padding: 0;
}

#app {
  margin: 0 auto;
  padding: 10px;
  width: 650px;
  height: 100vh;

  font-size: 16px;
  background-color: #e5e5e5;

position: relative;
}

h1, h2, h3, h4, h5, h6 {
  margin: 0;
}

p {
  margin: 0;
}

ul {
  padding: 0;
  list-style: none;
}

.btn {
  background: none;
  border: none;
  cursor: pointer;
}

.btn:hover {
  background: #bebeff;
  border-radius: 5px;
}
</style>
