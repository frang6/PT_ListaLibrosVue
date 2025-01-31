<template>
  <h1>Lista de Libros Disponibles</h1>
  <div class="container">
    <CartaLibro v-for="(elemento, index) in books.library" :key="index" :elemento="elemento" /> 
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import CartaLibro from "./CartaLibro.vue";
import booksData from '@/path/books.json'; 

const books = ref({ library: [] });

onMounted(() => {
  books.value = booksData;
});
</script>

<style scoped>
.container {
  display: flex;
  flex-wrap: wrap;
  gap: 20px;
  padding: 20px;
}
h1 {
  text-align: center;
  margin: 20px 0;
  font-size: 2em;
  font-weight: bolder;
}
</style>
