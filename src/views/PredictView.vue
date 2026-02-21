<template>
  <div class="container mt-4">
    <h3>Predicción de Churn (Abandono)</h3>
    <div class="row">
      <div class="col-md-6">
        <input v-model="cliente.tenure" type="number" placeholder="Meses de antigüedad" />
        <input v-model="cliente.MonthlyCharges" type="number" placeholder="Cargo Mensual" />
        <button @click="checkRisk" class="btn btn-warning mt-3">Calcular Riesgo</button>
      </div>

      <div
        v-if="resultado"
        class="col-md-6 alert"
        :class="resultado.churn ? 'alert-danger' : 'alert-success'"
      >
        <h4>Probabilidad: {{ resultado.probability }}%</h4>
        <p>{{ resultado.churn ? 'Riesgo Crítico de Fuga' : 'Cliente Estable' }}</p>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, reactive } from 'vue'
import axios from 'axios'

const cliente = reactive({
  tenure: 0,
  MonthlyCharges: 0,
  // ... todos los campos del modelo
})
const resultado = ref(null)

const checkRisk = async () => {
  const response = await axios.post('http://localhost:8000/api/predict/', cliente)
  resultado.value = response.data
}
</script>
