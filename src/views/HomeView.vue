<script setup>
import { ref, onMounted } from 'vue'

const poemasTraducidos = ref([])
const mostrarPoema = ref(false)

async function obtenerYTraducirPoemas() {
  try {
    const response = await fetch('https://poetrydb.org/author/All')
    const poemas = await response.json()

    const indiceAleatorio = Math.floor(Math.random() * poemas.length);
    const poemaSeleccionado = poemas[indiceAleatorio];

    const promesas = [
      {
        titulo: poemaSeleccionado.title,
        autor: poemaSeleccionado.author,
        texto: poemaSeleccionado.lines.join('\n'),
      }
    ]

    poemasTraducidos.value = await Promise.all(promesas)
  } catch (error) {
    console.error('Error:', error)
  }
}


onMounted(() => {
  obtenerYTraducirPoemas()
})
</script>

<template>
  <div class="container p-4 d-flex justify-content-center align-items-center flex-column"> 
    <h1 class="text-center mb-4 text-white">Poema de esta vez ❤️ para Nadia el amor de mi vida, razón de mi existir</h1>
    <button @click="mostrarPoema = !mostrarPoema" class="btn btn-danger mb-4">{{ mostrarPoema ? 'Ocultar poema' : 'Mostrar poema' }}</button> 
    <transition name="fade">
      <div v-if="mostrarPoema" class="poema card p-4 shadow-lg mb-4 bg-light"> 
        <h3 class="card-title text-center display-4 font-italic">{{ poemasTraducidos[0].titulo }}</h3>
        <h3 class="card-subtitle text-muted text-center mb-3 font-weight-light">{{ poemasTraducidos[0].autor }}</h3>
        <p class="card-text lead text-justify">{{ poemasTraducidos[0].texto }}</p>
      </div>
    </transition>
  </div>
</template>


<style scoped>
.poema {
  margin-bottom: 20px;
}

/* Transiciones */
.fade-enter-active, .fade-leave-active {
  transition: opacity 0.5s, background-color 0.5s;
}
.fade-enter, .fade-leave-to {
  opacity: 0;
}
</style>

