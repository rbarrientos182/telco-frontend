<template>
  <div class="container-fluid mt-4">
    <div class="d-flex justify-content-between align-items-center mb-4">
      <h2><i class="bi bi-speedometer2"></i> Monitor de Riesgo - Telmex Izúcar</h2>
      <button @click="fetchClientes" class="btn btn-outline-primary">Actualizar Datos</button>
    </div>

    <div class="row">
      <div class="col-md-4">
        <div class="card bg-danger text-white mb-4 shadow">
          <div class="card-body">
            <h5>Clientes en Riesgo Crítico</h5>
            <h2>{{ clientesRiesgo.length }}</h2>
          </div>
        </div>
      </div>
    </div>

    <div class="card shadow">
      <div class="card-body">
        <table class="table table-hover">
          <thead class="table-dark">
            <tr>
              <th>Cliente ID</th>
              <th>Antigüedad (Meses)</th>
              <th>Cargo Mensual</th>
              <th>Probabilidad de Fuga</th>
              <th>Estatus</th>
              <th>Acción</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="c in listaClientes" :key="c.id" :class="getFilaColor(c.probabilidad)">
              <td>{{ c.id }}</td>
              <td>{{ c.tenure }}</td>
              <td>${{ c.MonthlyCharges }}</td>
              <td>
                <div class="progress" style="height: 20px">
                  <div
                    class="progress-bar"
                    role="progressbar"
                    :style="{
                      width: c.probabilidad + '%',
                      backgroundColor: getBarColor(c.probabilidad),
                    }"
                  >
                    {{ c.probabilidad }}%
                  </div>
                </div>
              </td>
              <td>
                <span class="badge" :class="getBadgeClass(c.probabilidad)">
                  {{
                    c.probabilidad > 70 ? 'CRÍTICO' : c.probabilidad > 40 ? 'PREVENTIVO' : 'ESTABLE'
                  }}
                </span>
              </td>
              <td>
                <button class="btn btn-sm btn-light border">Ver Detalles</button>
              </td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed, onMounted } from 'vue'
import axios from 'axios'

const listaClientes = ref([])

const fetchClientes = async () => {
  try {
    const response = await axios.get('http://localhost:8000/api/predict/list-all/')
    listaClientes.value = response.data
  } catch (error) {
    console.error('Error cargando el Dashboard', error)
  }
}

const getFilaColor = (prob) => {
  if (prob > 70) return 'table-danger'
  if (prob > 40) return 'table-warning'
  return ''
}

const getBarColor = (prob) => {
  if (prob > 70) return '#dc3545' // Rojo
  if (prob > 40) return '#ffc107' // Amarillo
  return '#198754' // Verde
}

const getBadgeClass = (prob) => {
  if (prob > 70) return 'bg-danger'
  if (prob > 40) return 'bg-warning text-dark'
  return 'bg-success'
}

onMounted(fetchClientes)
</script>
