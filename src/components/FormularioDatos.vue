//componente que manejara el formilario y se activa 
//un evento al enviar los datos
<template>
  <form @submit.prevent="enviarDatos" class="rfc-form">
    <div class="form-group">
      <label for="nombre">Nombre:</label>
      <input type="text" id="nombre" v-model="nombre" required class="form-input" placeholder="Tu nombre">
    </div>

    <div class="form-group">
      <label for="apellidoPaterno">Apellido Paterno:</label>
      <input type="text" id="apellidoPaterno" v-model="apellidoPaterno" required class="form-input" placeholder="Tu apellido paterno">
    </div>

    <div class="form-group">
      <label for="apellidoMaterno">Apellido Materno:</label>
      <input type="text" id="apellidoMaterno" v-model="apellidoMaterno" required class="form-input" placeholder="Tu apellido materno">
    </div>

    <div class="form-group">
      <label for="fechaNacimiento">Fecha de Nacimiento:</label>
      <input type="date" id="fechaNacimiento" v-model="fechaNacimiento" required class="form-input">
    </div>

    <button type="submit" class="submit-button">Generar RFC</button>
  </form>
</template>

<script>
export default {
  // 1. Nombre del componente
  name: 'FormularioDatos',

  // 2. Variables de datos reactivas
  data() {
    return {
      nombre: '',
      apellidoPaterno: '',
      apellidoMaterno: '',
      fechaNacimiento: '',
    };
  },

  // 3. Lógica del componente
  methods: {
    enviarDatos() {
      // 3.1 Validar que los campos no estén vacíos antes de emitir.
      if (!this.nombre || !this.apellidoPaterno || !this.apellidoMaterno || !this.fechaNacimiento) {
        alert('Por favor, completa todos los campos.');
        return;
      }

      // 3.2 Emitir un evento con los datos del formulario.
      // Aquí usamos "datos-listos" para que el componente padre (App.vue) lo escuche.
      this.$emit('datos-listos', {
        nombre: this.nombre,
        apellidoPaterno: this.apellidoPaterno,
        apellidoMaterno: this.apellidoMaterno,
        fechaNacimiento: this.fechaNacimiento,
      });

      // 3.3 Opcional: Limpiar el formulario después de enviar.
      this.nombre = '';
      this.apellidoPaterno = '';
      this.apellidoMaterno = '';
      this.fechaNacimiento = '';
    },
  },
};
</script>

<style scoped>
/* Estilos específicos para este componente */
.rfc-form {
  max-width: 400px;
  margin: 20px auto;
  padding: 25px;
  border: 1px solid #ddd;
  border-radius: 10px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  background-color: #f9f9f9;
}

.form-group {
  margin-bottom: 20px;
}

label {
  display: block;
  margin-bottom: 8px;
  font-weight: bold;
  color: #555;
  text-align: left;
}

.form-input {
  width: 100%;
  padding: 12px;
  border: 1px solid #ccc;
  border-radius: 6px;
  box-sizing: border-box;
  font-size: 1em;
  transition: border-color 0.3s;
}

.form-input:focus {
  border-color: #42b983;
  outline: none;
}

.submit-button {
  width: 100%;
  padding: 12px;
  background-color: #42b983;
  color: white;
  border: none;
  border-radius: 6px;
  cursor: pointer;
  font-size: 1.1em;
  font-weight: bold;
  transition: background-color 0.3s ease;
}

.submit-button:hover {
  background-color: #369c6f;
}
</style>