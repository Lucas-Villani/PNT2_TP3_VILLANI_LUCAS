<template>
  <div>
    <h2>Formulario</h2>
    <form @submit.prevent="agregarUsuario" novalidate>
      <div class="mb-3">
        <label>Nombre</label>
        <input v-model="nombre" type="text" class="form-control" />
        <div v-if="nombreError" class="text-danger">{{ nombreError }}</div>
      </div>

      <div class="mb-3">
        <label>Edad</label>
        <input v-model.number="edad" type="number" class="form-control" />
        <div v-if="edadError" class="text-danger">{{ edadError }}</div>
      </div>

      <div class="mb-3">
        <label>Email</label>
        <input v-model="email" type="email" class="form-control" />
        <div v-if="emailError" class="text-danger">{{ emailError }}</div>
      </div>

      <button :disabled="!formValido" class="btn btn-primary">Agregar</button>
    </form>

    <h3 class="mt-4">Usuarios ingresados</h3>
    <table class="table table-striped" v-if="usuarios.length">
      <thead>
        <tr>
          <th>Nombre</th>
          <th>Edad</th>
          <th>Email</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(u, index) in usuarios" :key="index">
          <td>{{ u.nombre }}</td>
          <td>{{ u.edad }}</td>
          <td>{{ u.email }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  data() {
    return {
      nombre: '',
      edad: '',
      email: '',
      usuarios: []
    }
  },
  computed: {
    nombreError() {
      if (!this.nombre) return 'Nombre requerido';
      if (this.nombre.length < 5 || this.nombre.length > 15) return 'Nombre entre 5 y 15 caracteres';
      return null;
    },
    edadError() {
      if (!this.edad && this.edad !== 0) return 'Edad requerida';
      if (this.edad < 18 || this.edad > 120) return 'Edad entre 18 y 120';
      return null;
    },
    emailError() {
      if (!this.email) return 'Email requerido';
      return null;
    },
    formValido() {
      return !this.nombreError && !this.edadError && !this.emailError;
    }
  },
  methods: {
    agregarUsuario() {
      if (this.formValido) {
        this.usuarios.push({
          nombre: this.nombre,
          edad: this.edad,
          email: this.email
        });
        this.nombre = '';
        this.edad = '';
        this.email = '';
      }
    }
  }
}
</script>
