<template>
  <div id="formulario-persona">
    <form @submit.prevent="sendData" action="">
      <div class="container">
        <div class="row">
          <div class="col-md-4">
            <div class="form-group">
              <label for="">Nombre</label>
              <input
                ref="nombre"
                v-model="persona.nombre"
                type="text"
                class="form-control"
                :class="{ 'is-invalid': proccessing && nombreInvalido }"
                @focus="resetState"
                @keypress="resetState"
              />
            </div>
            <div class="form-group">
              <label for="">Apellido</label>
              <input
                v-model="persona.apellidos"
                type="text"
                class="form-control"
                :class="{ 'is-invalid': proccessing && apellidoInvalido }"
                @focus="resetState"
              />
            </div>
            <div class="form-group">
              <label for="">Email</label>
              <input
                v-model="persona.email"
                type="email"
                class="form-control"
                :class="{ 'is-invalid': proccessing && emailInvalido }"
                @focus="resetState"
              />
            </div>
          </div>
        </div>
        <div class="row">
          <div class="col-md-4">
            <div class="form-group">
              <button class="btn btn-primary">Añadir persona</button>
            </div>
          </div>
        </div>
      </div>
      <div class="container">
        <div class="row">
          <div class="col-md-12">
            <div
              v-if="error && proccessing"
              class="alert alert-danger"
              role="alert"
            >
              Debes rellenar todos los campos, melón.
            </div>
            <div v-if="correct" class="alert alert-success" role="alert">
              La persona has been added!
            </div>
          </div>
        </div>
      </div>
    </form>
  </div>
</template>

<script>
export default {
  name: "formulario-persona",
  data() {
    return {
      proccessing: false,
      correct: false,
      error: false,

      persona: {
        nombre: "",
        apellidos: "",
        email: "",
      },
    };
  },
  methods: {
    sendData() {
      this.proccessing = true;
      this.resetState();

      if (this.nombreInvalido || this.apellidoInvalido || this.emailInvalido) {
        this.error = true;
        return;
      }

      this.$emit("add-persona", this.persona);
      this.$refs.nombre.focus();

      this.error = false;
      this.correct = true;
      this.proccessing = false;

      this.persona = {
        nombre: "",
        apellidos: "",
        email: "",
      };
    },
    resetState() {
      this.correct = false;
      this.error = false;
    },
  },
  computed: {
    nombreInvalido() {
      return this.persona.nombre.length < 1;
    },
    apellidoInvalido() {
      return this.persona.apellidos.length < 1;
    },
    emailInvalido() {
      return this.persona.email.length < 1;
    },
  },
};
</script>

<style scoped>
form {
  margin-bottom: 2rem;
}
</style>
