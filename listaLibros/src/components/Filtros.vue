<template>
    <div class="filters">
        <!-- Obtenido de uiverse -->
        <div class="container">
            <div class="search-container">
                <input class="input" type="text" v-model="busquedaLibro" @input="$emit('busqueda', busquedaLibro)"
                    placeholder="Buscar por título o sinopsis..." />
                <svg viewBox="0 0 24 24" class="search__icon">
                    <g>
                        <path
                            d="M21.53 20.47l-3.66-3.66C19.195 15.24 20 13.214 20 11c0-4.97-4.03-9-9-9s-9 4.03-9 9 4.03 9 9 9c2.215 0 4.24-.804 5.808-2.13l3.66 3.66c.147.146.34.22.53.22s.385-.073.53-.22c.295-.293.295-.767.002-1.06zM3.5 11c0-4.135 3.365-7.5 7.5-7.5s7.5 3.365 7.5 7.5-3.365 7.5-7.5 7.5-7.5-3.365-7.5-7.5z">
                        </path>
                    </g>
                </svg>
            </div>
        </div>

        <div class="genero-filter">
  <svg xmlns="http://www.w3.org/2000/svg" width="100" height="100" viewBox="0 0 100 100" preserveAspectRatio="xMidYMid meet">
    <path stroke-width="4" stroke-linejoin="round" stroke-linecap="round" fill="none" d="M60.7,53.6L50,64.3m0,0L39.3,53.6M50,64.3V35.7m0,46.4A32.1,32.1,0,1,1,82.1,50A32.1,32.1,0,0,1,50,82.1Z" class="svg-stroke-primary"></path>
  </svg>
  <select id="genero" v-model="genero" @change="$emit('seleccionGenero', genero)">
    <option value="">Todos</option>
    <option value="Ciencia ficción">Ciencia ficción</option>
    <option value="Fantasía">Fantasía</option>
    <option value="Zombies">Zombies</option>
    <option value="Terror">Terror</option>
  </select>
</div>


        <!-- Obtenido de uiverse -->
        <div class="PB-range-slider-div">
            <label for="pages">Páginas: {{ pages }}</label>
            <input id="pages" class="PB-range-slider" type="range" min="0" max="2000" v-model="pages"
                @input="$emit('seleccionMaxPages', pages)" />
        </div>
    </div>
</template>

<script setup>
import { ref, watch } from 'vue';

const props = defineProps({
    busquedaLibroTerm: String,
    seleccionGenero: String,
    maxPages: Number
});

// Inicializamos las variables con los valores de las props
const busquedaLibro = ref(props.busquedaLibroTerm || '');
const genero = ref(props.seleccionGenero || '');
const pages = ref(props.maxPages || 1000);

// Observamos cambios en los valores locales y emitimos eventos actualizados
watch(busquedaLibro, (newValue) => {
    emit('busqueda', newValue);
});

watch(genero, (newValue) => {
    emit('seleccionGenero', newValue);
});

watch(pages, (newValue) => {
    emit('seleccionMaxPages', newValue);
});

// Lista de géneros disponibles
const generos = ["Fantasía", "Ciencia ficción", "Terror", "Zombies"];
</script>

<style scoped>

.filters {
    display: flex;
    gap: 1rem;
    padding: 1rem;
    justify-content: center;
}


/* From Uiverse.io by Smit-Prajapati */ 
.container {
  position: relative;
  background: linear-gradient(135deg, rgb(179, 208, 253) 0%, rgb(164, 202, 248) 100%);
  border-radius: 1000px;
  padding: 10px;
  display: grid;
  place-content: center;
  z-index: 0;
  max-width: 300px;
  margin: 0 10px;
}

.search-container {
  position: relative;
  width: 100%;
  border-radius: 50px;
  background: linear-gradient(135deg, rgb(218, 232, 247) 0%, rgb(214, 229, 247) 100%);
  padding: 5px;
  display: flex;
  align-items: center;
}

.search-container::after, .search-container::before {
  content: "";
  width: 100%;
  height: 100%;
  border-radius: inherit;
  position: absolute;
}

.search-container::before {
  top: -1px;
  left: -1px;
  background: linear-gradient(0deg, rgb(218, 232, 247) 0%, rgb(255, 255, 255) 100%);
  z-index: -1;
}

.search-container::after {
  bottom: -1px;
  right: -1px;
  background: linear-gradient(0deg, rgb(163, 206, 255) 0%, rgb(211, 232, 255) 100%);
  box-shadow: rgba(79, 156, 232, 0.7019607843) 3px 3px 5px 0px, rgba(79, 156, 232, 0.7019607843) 5px 5px 20px 0px;
  z-index: -2;
}

.input {
  padding: 10px;
  width: 100%;
  background: linear-gradient(135deg, rgb(218, 232, 247) 0%, rgb(214, 229, 247) 100%);
  border: none;
  color: #9EBCD9;
  font-size: 20px;
  border-radius: 50px;
}

.input::placeholder {
  font-size: 0.8em;
}

.input:focus {
  outline: none;
  background: linear-gradient(135deg, rgb(239, 247, 255) 0%, rgb(214, 229, 247) 100%);
}

.search__icon {
  width: 50px;
  aspect-ratio: 1;
  border-left: 2px solid white;
  border-top: 3px solid transparent;
  border-bottom: 3px solid transparent;
  border-radius: 50%;
  padding-left: 12px;
  margin-right: 10px;
}

.search__icon:hover {
  border-left: 3px solid white;
}

.search__icon path {
  fill: white;
}

/* Estilo para el contenedor */
.genero-filter {
  position: relative;
  width: 16rem; /* 64px en Tailwind */
  background-color: #f9fafb; /* bg-gray-50 */
  border-radius: 0.5rem; /* rounded-lg */
  overflow: hidden;
}

/* Efecto antes del contenedor (el círculo violeta con el blur) */
.genero-filter::before {
  content: '';
  position: absolute;
  width: 3rem; /* 12 en Tailwind */
  height: 3rem; /* 12 en Tailwind */
  background-color: #7c3aed; /* bg-violet-500 */
  border-radius: 9999px; /* rounded-full */
  top: 0;
  right: 0;
  filter: blur(10px);
  box-shadow: -60px 20px 10px 10px rgba(249, 176, 185, 1); /* box-shadow */
  z-index: -1; /* Asegura que no se ponga encima del contenido */
}

/* Estilo para el SVG */
.genero-filter svg {
  position: absolute;
  top: 0.375rem; /* top-1.5 en Tailwind */
  right: 0;
  width: 2rem; /* 8 en Tailwind */
  height: 2rem; /* 8 en Tailwind */
  transform: rotate(-45deg); /* -rotate-45 */
  stroke: #fbcfe8; /* stroke-pink-300 */
  transition: transform 0.3s;
}

.genero-filter:hover svg {
  transform: rotate(0deg); /* Cuando se pasa el ratón, se rota */
}

/* Estilo para el select */
.genero-filter select {
  appearance: none;
  background-color: transparent;
  border: 1px solid #6b7280; /* border-neutral-500 */
  color: #3b82f6; /* text-pink-400 */
  font-size: 0.875rem; /* text-sm */
  font-weight: 700; /* font-bold */
  padding: 0.625rem 1rem; /* p-2.5 en Tailwind */
  width: 100%;
  border-radius: 0.5rem; /* rounded-lg */
  outline: none;
  cursor: pointer;
  transition: border-color 0.3s, box-shadow 0.3s;
  position: relative;
  z-index: 1;
}

/* Estilo para el borde cuando el select está en focus */
.genero-filter select:focus {
  border-color: #7c3aed; /* focus:border-violet-500 */
  box-shadow: 0 0 0 2px rgba(124, 58, 237, 0.3); /* focus:ring-violet-500 */
}

/* Estilo para las opciones del select */
.genero-filter select option {
  color: #1f2937; /* text-neutral-900 */
  background-color: #fff; /* Blanco de fondo para las opciones */
  padding: 0.5rem 1rem;
  font-size: 0.875rem; /* text-sm */
  font-weight: 700; /* font-bold */
  transition: background-color 0.3s;
}

/* Estilo para cuando el usuario pasa el ratón sobre una opción */
.genero-filter select option:hover {
  background-color: #d1d5db; /* Fondo gris claro en hover */
}

/* Estilo para cuando el select está abierto (desplegable) */
.genero-filter select:focus option {
  background-color: #f9fafb; /* Fondo suave al hacer focus */
}


/* From Uiverse.io by satisshTechie */ 
.PB-range-slider {
  -webkit-appearance: none;
  width: 100%;
  height: 4px;
  border-radius: 5px;
  background: #D5DBE1;
  outline: none;
  opacity: 0.7;
  -webkit-transition: .2s;
  transition: opacity .2s;
}

.PB-range-slider::-webkit-slider-thumb {
  -webkit-appearance: none;
  appearance: none;
  width: 15px;
  height: 15px;
  border-radius: 50%;
  background-color: #000000;
  cursor: pointer;
  transition: 0.3s ease-in-out;
}

.PB-range-slider::-webkit-slider-thumb:hover {
  box-shadow: 0px 0px 0px 8px rgba(0, 0, 0, 0.16);
  transition: 0.3s ease-in-out;
}

.PB-range-slider::-moz-range-thumb {
  width: 15px;
  height: 15px;
  border-radius: 50%;
  background-color: #000000;
  cursor: pointer;
}

.PB-range-slider-div {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 1rem;
  padding: 1rem;
  border-radius: 6px;
  border: 1px solid #C6CACE;
  box-shadow: 0px 1px 2px 0px #1F1E241F;
}

.PB-range-slidervalue {
  font-weight: 600;
}
</style>