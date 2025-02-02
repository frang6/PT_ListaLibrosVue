<template>
  <div class="card" @click="emitirClick">
    <img :src="libro.cover" :alt="libro.title">
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

.card{
  background-color: rgb(255, 255, 255);
  border-radius: 8px;
  box-shadow: 0 7px 15px rgba(0, 0, 0, 0.1);
  cursor: pointer;
  overflow: hidden;
  transition: transform 0.2s;
  width: 150px;
}

.card:hover{
  transform: scale(1.05);
}

img{
  max-width: 100%;
  height: auto;
  border-radius: 8px;
  padding: 5px;
}


</style>
