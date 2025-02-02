<template>
  <div>
    <h2>Libros Disponibles</h2>
    <nav>
      <Filtros :busquedaLibroTerm="busquedaLibro" 
    :seleccionGenero="seleccionGenero" 
    :maxPages="maxPages"
      @busqueda="busquedaLibro = $event" 
      @seleccionGenero="seleccionGenero = $event"
      @seleccionMaxPages="maxPages = $event" />
    </nav>
    

    <div class="container">
      <CartaLibro v-for="(libro, index) in librosFiltrados" :key="index" :libro="libro" @click="mover(libro)" class="cartas" />
    </div>
  </div>
</template>

<script setup>
import { ref, computed, toRefs, defineProps, defineEmits } from 'vue';
import CartaLibro from './CartaLibro.vue';
import Filtros from './Filtros.vue';

const props = defineProps({ libros: Array }); // Recibimos libros desde el padre
const { libros } = toRefs(props); // Convertimos a una referencia reactiva

const emit = defineEmits(["mover"]);

const busquedaLibro = ref('');
const seleccionGenero = ref('');
const maxPages = ref(1000);

const librosFiltrados = computed(() => {
  return (libros.value || []).filter(libro => { // Aseguramos que libros.value no sea undefined
    const coincideBusqueda = busquedaLibro.value === '' ||
      libro.title.toLowerCase().includes(busquedaLibro.value.toLowerCase()) ||
      libro.synopsis.toLowerCase().includes(busquedaLibro.value.toLowerCase());

    const coincideGenero = seleccionGenero.value === '' || libro.genre === seleccionGenero.value;
    const coincidePaginas = libro.pages <= maxPages.value;

    return coincideBusqueda && coincideGenero && coincidePaginas;
  });
});

const mover = (libro) => {
  emit("mover", libro);
};
</script>



<style scoped>

.container {
  display: flex;
  flex-wrap: wrap;
  gap: 1rem;
  padding: 1rem;
  width: 1200px;
  margin: 0 auto;
}

h2{
  text-align: center;
  margin: 1rem;
}


</style>
