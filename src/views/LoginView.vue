<template>
  <div class="container mt-5">
    <div class="row justify-content-center">
      <div class="col-md-4 card p-4 shadow">
        <h2 class="text-center mb-4">Acceso Telmex</h2>
        <form @submit.prevent="handleLogin">
          <div class="mb-3">
            <label>Usuario</label>
            <input v-model="form.username" type="text" class="form-control" required />
          </div>
          <div class="mb-3">
            <label>Contraseña</label>
            <input v-model="form.password" type="password" class="form-control" required />
          </div>
          <button type="submit" class="btn btn-primary w-100">Entrar al Sistema</button>
        </form>
      </div>
    </div>
  </div>
</template>

<script setup>
import { reactive } from 'vue'
import { useAuthStore } from '../stores/auth'
import { useRouter } from 'vue-router'

const form = reactive({ username: '', password: '' })
const auth = useAuthStore()
const router = useRouter()

const handleLogin = async () => {
  const success = await auth.login(form)
  if (success) {
    router.push('/predict') // Redirigir al formulario de IA
  } else {
    alert('Credenciales incorrectas')
  }
}
</script>
