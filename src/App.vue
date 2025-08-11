<template>
  <h1>Registro de Gastos de Camiones</h1>

  <form @submit.prevent="agregarGasto">
    <label>Camión:</label>
    <input v-model="camion" placeholder="Ej: Camión 1" />

    <label>Fecha:</label>
    <input type="date" v-model="fecha" />

    <label>Tipo de gasto:</label>
    <input v-model="tipo" placeholder="Ej: Combustible" />

    <label>Monto:</label>
    <input type="number" v-model="monto" />

    <button type="submit">Agregar gasto</button>
  </form>

  <hr />

  <ul>
    <li v-for="gasto in gastos" :key="gasto.id">
      {{ gasto.camion }} - {{ gasto.fecha }} - {{ gasto.tipo }} - ${{ gasto.monto }}
    </li>
  </ul>
</template>

<script setup>
import { ref } from 'vue'

const camion = ref('')
const fecha = ref('')
const tipo = ref('')
const monto = ref('')
const gastos = ref([])

function agregarGasto() {
  if (!camion.value || !fecha.value || !tipo.value || !monto.value) {
    alert('Todos los campos son obligatorios')
    return
  }

  gastos.value.push({
    id: Date.now(),
    camion: camion.value,
    fecha: fecha.value,
    tipo: tipo.value,
    monto: parseFloat(monto.value)
  })

  // Limpiar campos
  camion.value = ''
  fecha.value = ''
  tipo.value = ''
  monto.value = ''
}
</script>

<style scoped>
form {
  display: flex;
  flex-direction: column;
  max-width: 300px;
}
label {
  margin-top: 10px;
}
input, button {
  padding: 5px;
  margin-top: 5px;
}
</style>
