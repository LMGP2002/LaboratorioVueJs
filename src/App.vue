<script setup lang="ts">
import Formulario from './components/Formulario.vue';
</script>

<template>
    <main class="main">
      <Formulario></Formulario>
    </main>
</template>

<style>
  *{
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }

 .main{
    height: 100vh;
    width: 100vw;
    display: grid;
    grid-template-columns: repeat(2, 1fr);
      
  }


</style>
