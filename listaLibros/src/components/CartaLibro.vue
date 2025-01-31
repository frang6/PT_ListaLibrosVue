<template>
  <div class="card" @click="emitirClick">
    <img :src="libro.cover" :alt="libro.title" class="cover">
    <div class="info">
      <h2>{{ libro.title }}</h2>
      <p>{{ libro.synopsis }}</p>
      <p><strong>Autor:</strong> {{ libro.author.name }}</p>
      <p><strong>Publicado en:</strong> {{ libro.year }}</p>
    </div>
  </div>
</template>

<script setup>
import { defineProps, defineEmits } from "vue";

const props = defineProps({ libro: Object });
const emit = defineEmits(["click"]);

const emitirClick = () => {
  emit("click", props.libro); 
};
</script>

<style scoped>
.card {
  width: 250px;
  border: 1px solid #ddd;
  border-radius: 8px;
  overflow: hidden;
  box-shadow: 2px 2px 10px rgba(0, 0, 0, 0.1);
  cursor: pointer;
  transition: transform 0.2s;
}
.card:hover {
  transform: scale(1.05);
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
