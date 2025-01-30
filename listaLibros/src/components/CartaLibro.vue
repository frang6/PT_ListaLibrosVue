<template>
  <div class="container">
    <div v-for="(elemento, index) in books.library" :key="index" class="card">
      <img :src="elemento.book.cover" :alt="elemento.book.title" class="cover">
      <div class="info">
        <h2>{{ elemento.book.title }}</h2>
        <p>{{ elemento.book.synopsis }}</p>
        <p><strong>Autor:</strong> {{ elemento.book.author.name }}</p>
        <p><strong>Publicado en:</strong> {{ elemento.book.year }}</p>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
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
.card {
  width: 250px;
  border: 1px solid #ddd;
  border-radius: 8px;
  overflow: hidden;
  box-shadow: 2px 2px 10px rgba(0, 0, 0, 0.1);
}
.cover {
  width: 100%;
  height: 300px;
  object-fit: cover;
}
.info {
  padding: 10px;
}
</style>
