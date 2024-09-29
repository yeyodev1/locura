<script setup>
import HomeView from './views/HomeView.vue';
</script>

<template>
  <div class="principal">
    <HomeView/>
  </div>
</template>

<style scoped>
.principal {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  width: 100%;
  height: 100vh;
  background-repeat: no-repeat;
  background-size: cover; /* Asegura que la imagen cubra todo el fondo */
  background-position: center; /* Centra la imagen */
  background-image: url("https://i.pinimg.com/564x/e3/5c/5d/e35c5d22fb28d06569f2a8871b272740.jpg");
}
</style>