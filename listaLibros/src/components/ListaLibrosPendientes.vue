<template>
    <div class="lista-libros">
      <h2>Lista de Lectura</h2>
      <div class="libros-container">
        <CartaLibro
          v-for="libro in libros"
          :key="libro.ISBN"
          :libro="libro"
          @agregarAListaPendientes="agregarAListaPendientes"
        />
      </div>
    </div>
  </template>
  
  <script>
  import CartaLibro from "./CartaLibro.vue";
  
  export default {
    props: {
      libros: Array,
    },
    components: {
      CartaLibro,
    },
    methods: {
      eliminarDeListaPendientes(libro) {
        this.$emit("eliminarDeListaPendientes", libro);
      },
    },
  };
  </script>
  
  <style scoped>
  .lista-libros {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-around;
  }
  
  .libros-container {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
  }
  </style>
  