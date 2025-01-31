<template>
  <div class="card">
    <img :src="elemento.book.cover" :alt="elemento.book.title" class="cover" />
    <div class="info">
      <h2>{{ elemento.book.title }}</h2>
      <p>{{ elemento.book.synopsis }}</p>
      <p><strong>Autor:</strong> {{ elemento.book.author.name }}</p>
      <p><strong>Publicado en:</strong> {{ elemento.book.year }}</p>
    </div>
  </div>
</template>

<script setup>
defineProps({
  elemento: Object,
});
</script>

<style scoped>
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
  font-size: 0.9em;
}

h2 {
  font-size: 1.4em;
  margin: 0;
  font-weight: bolder;
}
</style>
