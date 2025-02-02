<template>
  <header>
    <h1>Biblioteca Jandula</h1>
  </header>

  <main id="contenedor">
    <GestorLibros />
  </main>
  
  <footer>
    <h3>Realizado por <a href="https://github.com/frang6">Fran Garcia</a> </h3>
  </footer>
</template>

  

<script setup>
  import GestorLibros from './components/GestorLibros.vue';
</script>
  
  
  
<style scoped>

@keyframes gradientAnimation {
    0% {
        background-position: 0% 50%;
    }
    50% {
        background-position: 100% 50%;
    }
    100% {
        background-position: 0% 50%;
    }
}

header, footer {
    background: linear-gradient(270deg, #0e10a1, #54ccf0, #002280);
    background-size: 400% 400%;
    animation: gradientAnimation 10s ease infinite;
    color: #fff;
    padding: 1rem;
    width: 100%;
    text-align: center;
    box-shadow: 0 7px 15px rgba(0, 0, 0, 0.3);
}

a {
    color: #fff;
    text-decoration: none;
}

a:hover {
    text-decoration: underline;
    cursor: pointer;
}
h1{
  font-size: 3em;
}


    

</style>
  
  
