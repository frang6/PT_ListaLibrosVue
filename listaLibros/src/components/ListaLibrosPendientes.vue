<template>
  <div>
    <h2>Libros Pendientes</h2>
    <div class="container">
      <CartaLibro 
        v-for="(libro, index) in libros" 
        :key="index" 
        :libro="libro" 
        @click="devolver(libro)"
      />
    </div>
  </div>
</template>

<script setup>
import CartaLibro from './CartaLibro.vue';

defineProps({ libros: Array });
const emit = defineEmits(["devolver"]);

const devolver = (libro) => {
  emit("devolver", libro);
};
</script>

<style scoped>
.container {
  display: flex;
  flex-wrap: wrap;
  gap: 20px;
  padding: 20px;
}
</style>
