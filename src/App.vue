<template>
  <div id="app" class="container">
    <div class="row">
      <div class="col-md-12">
        <h1>Personas</h1>
      </div>
    </div>
    <div class="row">
      <div class="col-md-12">
        <FormularioPersona @add-persona="addPersona" />
        <TablaPersonas
          v-bind:personas="personas"
          @delete-persona="deletePersona"
          @actualizar-persona="actualizarPersona"
        />
      </div>
    </div>
  </div>
</template>

<script>
import TablaPersonas from "./components/TablaPersonas.vue";
import FormularioPersona from "./components/FormularioPersona.vue";

export default {
  // Name of the component
  name: "App",
  // Component dependencies
  components: {
    TablaPersonas,
    FormularioPersona,
  },
  // Component state variables
  data() {
    return {
      personas: [
        {
          id: 1,
          nombre: "Jon",
          apellidos: "Snow",
          email: "jonsnow@gmail.com",
        },
        {
          id: 2,
          nombre: "Tyrion",
          apellidos: "Lannister",
          email: "tyrion@gmail.com",
        },
        {
          id: 3,
          nombre: "Daennerys",
          apellidos: "Targaryen",
          email: "danny@gmail.com",
        },
      ],
    };
  },
  methods: {
    addPersona(persona) {
      // Crear id único
      let id = 0;
      // Si hay algo en el array...
      if (this.personas.length > 0) {
        // El id es igual al id de la longitud de array - 1 (el último id del array) + 1
        id = this.personas[this.personas.length - 1].id + 1;
      }
      // Ahora el array es el array existente + la persona que mandamos por form y la id que hemos creado.
      this.personas = [...this.personas, { ...persona, id }];
    },

    deletePersona(id) {
      // Filtra y devuelve todas las personas cuyo id sea distinto del id pasado por parámetros.
      this.personas = this.personas.filter((persona) => persona.id !== id);
    },
    actualizarPersona(id, personaActualizada) {
      this.personas = this.personas.map((persona) => {
        return persona.id === id ? personaActualizada : persona;
      });
    },
  },
};
</script>

<style>
#app {
  margin-top: 3em;
}

button {
  background: #009435;
  border: 1px solid #009435;
}
</style>
