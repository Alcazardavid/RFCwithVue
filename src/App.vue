//Este es el componente central que sirve como comunicador entre 
//formularioDatos y ResultadoRFC
<template>
  <div id = "app">
    <h1>generarRFC</h1>
    <FormularioDatos @datos-listos = "generarRFC"/>
    <ResultadoRFC :rfc="rfc"/>
  </div>
</template>

<script>
import FormularioDatos from './components/FormularioDatos.vue';
import ResultadoRFC from './components/ResultadoRFC.vue';

export default {
  name: 'App',
  components: {
    FormularioDatos,
    ResultadoRFC,
  },
  data(){
    return {
      rfc: '',
    };
  },
  methods: {
    generarRFC(datos){
      const apellidoPaterno = datos.apellidoPaterno.trim().toUpperCase();
      const apellidoMaterno = datos.apellidoMaterno.trim().toUpperCase();
      const nombres = datos.nombre.trim().toUpperCase().split(" "); // separar nombres

      // --- Obtener inicial del nombre ---
      let inicialNombre;
      if ((nombres[0] === "JOSE" || nombres[0] === "MARIA") && nombres.length > 1) {
        inicialNombre = nombres[1][0]; // segunda opción
      } else {
        inicialNombre = nombres[0][0];
      }

      //Obtener el primer caracter del apellido paterno y su segunda vocal
      let ApellidoPatInicial = apellidoPaterno[0];
        let primeraVocal = '';
        for (let i = 1; i < apellidoPaterno.length; i++) {
          if ("AEIOU".includes(apellidoPaterno[i])) {
            primeraVocal = apellidoPaterno[i];
            break;
          }
        }
        ApellidoPatInicial += primeraVocal;

      // --- Apellidos ---
      const Materno = apellidoMaterno.substring(0,1);

      // --- Fecha ---
      const [anioStr, mesStr, diaStr] = datos.fechaNacimiento.split('-');
      const anio = anioStr.substring(2);
      const mes = mesStr;
      const dia = diaStr;

      // --- Construcción del RFC ---
      const rfcGenerado = `${ApellidoPatInicial}${Materno}${inicialNombre}${anio}${mes}${dia}XXX`;

      // --- Guardamos en data ---
      this.rfc = rfcGenerado;
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
