<template>
    
    <section id="dispobibles">
          <ListaLibrosDisponibles 
          :libros="librosDisponibles" 
          @mover="moverLibro"
        />
      </section>
        
      <section id="pendientes"> 
        <ListaLibrosPendientes 
          :libros="librosPendientes" 
          @devolver="devolverLibro"
        />
    </section>
    
    
  </template>
  
  <script setup>
  import { ref, onMounted } from 'vue';
  import ListaLibrosDisponibles from './ListaLibrosDisponibles.vue';
  import ListaLibrosPendientes from './ListaLibrosPendientes.vue';
  import booksData from '@/path/books.json';
  
  
  const librosDisponibles = ref([]);
  const librosPendientes = ref([]);
  
  
  onMounted(() => {
    librosDisponibles.value = booksData.library.map(item => item.book);
  });
  
  
  const moverLibro = (libro) => {
    librosDisponibles.value = librosDisponibles.value.filter(b => b.ISBN !== libro.ISBN);
    librosPendientes.value.push(libro);
  };
  
  const devolverLibro = (libro) => {
    librosPendientes.value = librosPendientes.value.filter(b => b.ISBN !== libro.ISBN);
    librosDisponibles.value.push(libro);
  };
</script>
  
<style scoped>



  
</style>
  