<template>
  <div id="tabla-personas">
    <div v-if="!personas.length" class="alert alert-info">
      No hay personas agregadas a la lista.
    </div>
    <table class="table">
      <thead>
        <tr>
          <th>Nombre</th>
          <th>Apellidos</th>
          <th>Email</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="persona in personas" :key="persona.id">
          <td v-if="editando === persona.id">
            <input type="text" class="form-control" v-model="persona.nombre" />
          </td>
          <td v-else>
            {{ persona.nombre }}
          </td>
          <td v-if="editando === persona.id">
            <input
              type="text"
              class="form-control"
              v-model="persona.apellidos"
            />
          </td>
          <td v-else>
            {{ persona.apellidos }}
          </td>
          <td v-if="editando === persona.id">
            <input type="email" class="form-control" v-model="persona.email" />
          </td>
          <td v-else>
            {{ persona.email }}
          </td>
          <td v-if="editando === persona.id">
            <button class="btn btn-success" @click="guardarPersona(persona)">
              💾 Guardar
            </button>
            <button
              class="btn btn-secondary ml-2"
              @click="cancelarEdicion(persona)"
            >
              ❌ Cancelar
            </button>
          </td>
          <td v-else>
            <button class="btn btn-info" @click="editarPersona(persona)">
              ✏️ Editar
            </button>
            <button
              class="btn btn-danger ml-2"
              @click="$emit('delete-persona', persona.id)"
            >
              🗑️ Eliminar
            </button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  // Name of component
  name: "tabla-personas",
  // Props (like React props, define the "arguments" of the component)
  props: {
    personas: Array,
  },
  // State variables
  data() {
    return {
      editando: null,
    };
  },

  methods: {
    editarPersona(persona) {
      this.personaEditada = Object.assign({}, persona);
      this.editando = persona.id;
    },
    guardarPersona(persona) {
      if (
        !persona.nombre.length ||
        !persona.apellidos.length ||
        !persona.email.length
      ) {
        return;
      }
      this.$emit("actualizar-persona", persona.id, persona);
      this.editando = null;
    },
    cancelarEdicion(persona) {
      Object.assign(persona, this.personaEditada);
      this.editando = null;
    },
  },
};
</script>

<style scoped>
button {
  margin-left: 1em;
}
</style>
