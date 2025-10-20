<template>
  <div>
    <h2>Usuarios desde API</h2>
    <table class="table table-striped" v-if="usuarios.length">
      <thead>
        <tr>
          <th>Nombre</th>
          <th>Email</th>
          <th>Teléfono</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="usuario in usuarios" :key="usuario.id">
          <td>{{ usuario.nombre }}</td>
          <td>{{ usuario.email }}</td>
          <td>{{ usuario.telefono }}</td>
        </tr>
      </tbody>
    </table>
    <p v-else>Cargando usuarios...</p>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  data() {
    return {
      usuarios: []
    }
  },
  async created() {
    try {
      const response = await axios.get('https://68f6ae27f7fb897c66134c68.mockapi.io/usuarios')
      this.usuarios = response.data
    } catch (error) {
      console.error('Error al obtener usuarios:', error)
    }
  }
}
</script>
