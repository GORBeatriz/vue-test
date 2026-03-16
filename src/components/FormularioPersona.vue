<template>
  <div id="formulario-persona">
    <form @submit.prevent="enviarFormulario">
      <div class="container">
        <div class="row">
          <div class="col-md-4">
            <label>Nombre</label>
            <input
              ref="primer"
              v-model="persona.nombre"
              type="text"
              :class="{ 'is-invalid': procesando && nombreInvalido }"
              class="form-control"
              @focus="resetEstado"
              @keypress="resetEstado"
            />
          </div>

          <div class="col-md-4">
            <label>Apellido</label>
            <input
              v-model="persona.apellido"
              type="text"
              :class="{ 'is-invalid': procesando && apellidoInvalido }"
              class="form-control"
              @focus="resetEstado"
            />
          </div>

          <div class="col-md-4">
            <label>Email</label>
            <input
              v-model="persona.email"
              type="email"
              :class="{ 'is-invalid': procesando && emailInvalido }"
              class="form-control"
              @focus="resetEstado"
            />
          </div>
        </div>

        <div class="row">
          <div class="col-md-12">
            <p v-if="error && procesando" class="error-message">
              Por favor, rellena todos los campos correctamente
            </p>
          </div>

          <div class="col-md-4">
            <button class="btn btn-primary">Añadir persona</button>
          </div>
        </div>
      </div>
    </form>
  </div>
</template>

<script>
export default {
  name: 'formulario-persona',
  data() {
    return {
      procesando: false,
      error: false,
      persona: {
        id: null,
        nombre: '',
        apellido: '',
        email: '',
      },
    }
  },
  methods: {
    enviarFormulario() {
      this.procesando = true
      this.resetEstado()

      if (this.nombreInvalido || this.apellidoInvalido || this.emailInvalido) {
        this.error = true
        return
      }

      this.persona.id = this.generarNuevoId()
      this.$emit('add-persona', this.persona)
      this.$refs.primer.focus()
      this.persona = {
        id: null,
        nombre: '',
        apellido: '',
        email: '',
      }
      this.error = false
      this.procesando = false
    },
    resetEstado() {
      this.error = false
    },
    generarNuevoId() {
      return Math.floor(Math.random() * 1000000)
    },
  },
  computed: {
    nombreInvalido() {
      return this.persona.nombre === ''
    },
    apellidoInvalido() {
      return this.persona.apellido === ''
    },
    emailInvalido() {
      return this.persona.email === ''
    },
  },
}
</script>

<style scoped>
.error-message {
  color: red;
}
</style>