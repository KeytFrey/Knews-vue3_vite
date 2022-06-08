<script setup lang="ts">
import NewsView from './view/NewsView.vue';
</script>

<template>
  <Suspense>
    <NewsView />
  </Suspense>
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
  height: 100%;

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

input,
textarea {
  padding: 0;
  margin-bottom: 10px;
  min-width: 200px;
  width: 200px;
  height: 20px;
  border: none;
  background: none;
  border-bottom: 1px solid #bebeff;
  outline: none;
}


form {
  display: flex;
  justify-content: flex-end;
  flex-wrap: wrap;
  margin: 0 0 0 auto;
  width: 200px;
  height: auto;
}

.btn:hover {
  background: #bebeff;
  border-radius: 5px;
}
</style>
