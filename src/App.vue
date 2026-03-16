<template>
  <div id="app" class="container">
    <div class="row">
      <div class="col-md-12">
        <h1>Personas</h1>
      </div>
    </div>

    <div class="row">
      <div class="col-md-12">
        <!-- escucha el evento personalizado add-persona y, cuando ocurra, se ejecuta el método agregarPersona -->
        <formulario-persona @add-persona="agregarPersona" />
        <tabla-personas :personas="personas" @delete-persona="eliminarPersona" />
      </div>
    </div>
  </div>
</template>

<script>
import TablaPersonas from '@/components/TablaPersonas.vue';
import FormularioPersona from './components/FormularioPersona.vue';

export default {
  name: 'app',
  components: {
    TablaPersonas,
    FormularioPersona,
  },
  data() {
    return {
      personas: [
        {
          id: 1,
          nombre: 'Jon',
          apellido: 'Nieve',
          email: 'jon@email.com',
        },
        {
          id: 2,
          nombre: 'Tyrion',
          apellido: 'Lannister',
          email: 'tyrion@email.com',
        },
        {
          id: 3,
          nombre: 'Daenerys',
          apellido: 'Targaryen',
          email: 'daenerys@email.com',
        },
      ],
    }
  },
  /* se asigna un id único al elemento creado > añade un nuevo objeto al array 'personas' se usa el operador spread de propagación ..., 
  útil para combinar objetos y arrays, para crear un nuevo array que contenga los elemento antiguos del array personas junto con la nueva. */
  methods: {
  agregarPersona(persona) {
    let id = 0;
    
    if (this.personas.length > 0) {
      id = this.personas[this.personas.length - 1].id + 1;
    }
    
    this.personas= [...this.personas, { ...persona, id}];
  },
  eliminarPersona(id) {
    this.personas = this.personas.filter(
      persona => persona.id !== id
    );
  }
}

}

</script>

<style>
button {
  background: #009435;
  border: 1px solid #009435;
}
</style>