<script setup>
import { ref, onMounted } from 'vue'

const poemasTraducidos = ref([])

async function obtenerYTraducirPoemas() {
  try {
    const response = await fetch('http://poetrydb.org/author/All')
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
  <div class="container p-4"> 
    <h1 class="text-center mb-4">Poema de esta vez ❤️</h1>
    <div v-for="(poema, index) in poemasTraducidos" :key="index" class="poema card p-4 shadow-lg mb-4">
      <h3 class="card-title text-center display-4">{{ poema.titulo }}</h3>
      <h3 class="card-subtitle text-muted text-center mb-3">{{ poema.autor }}</h3>
      <p class="card-text lead">{{ poema.texto }}</p>
    </div>
  </div>
</template >


<style scoped>
.poema {
  margin-bottom: 20px;
}
</style>
