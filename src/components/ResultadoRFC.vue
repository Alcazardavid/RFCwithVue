//Este componente recibira el RFC como una propieda 
<template>
  <div class="rfc-result-container">
    <p v-if="rfc" class="rfc-display">
      Tu RFC es: <strong class="rfc-value">{{ rfc }}</strong>
    </p>
    <p v-else class="no-rfc-message">
      Ingresa tus datos para generar el RFC.
    </p>
  </div>
</template>

<script>
export default {
  // 1. Nombre del componente para facilitar la depuración
  name: 'ResultadoRfc',
  
  // 2. Propiedades (props)
  // Las "props" son la forma en que un componente padre le pasa información a un componente hijo.
  props: {
    rfc: {
      type: String,
      required: false, // El RFC no es requerido al inicio, ya que el formulario está vacío.
      default: '', // Valor predeterminado para evitar errores si la prop no está presente.
    },
  },
};
</script>

<style scoped>
/* Estilos específicos para este componente */
.rfc-result-container {
  margin-top: 20px;
  padding: 15px;
  border: 1px solid #dcdcdc;
  border-radius: 8px;
  background-color: #f9f9f9;
  box-shadow: 0 1px 3px rgba(0, 0, 0, 0.08);
}

.rfc-display {
  font-size: 1.2em;
  color: #333;
}

.rfc-value {
  color: #007bff; /* Un color que resalta el RFC */
  font-size: 1.3em;
  word-break: break-all; /* Para que el texto no se salga del contenedor en pantallas pequeñas */
}

.no-rfc-message {
  font-style: italic;
  color: #666;
}
</style>