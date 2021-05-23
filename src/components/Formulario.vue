<template>
  <section class="src-components-formulario">
    <div class="container ">
      <h2 class="titulo">Formulario</h2>
      <hr />

      <vue-form :state="formState" @submit.prevent="enviar()">
        <!-- ------------------------------------------------------------------------ -->
        <!-- Campo nombre -->
        <validate tag="div">
          <label for="nombre"><i>Nombre</i></label>
          <input
            type="text"
            id="nombre"
            name="nombre"
            class="form-control my-3"
            autocomplete="off"
            v-model.trim="formData.nombre"
            required
            :minlength="nombreLengthMin"
            :maxlength="nombreLengthMax"
            no-espacios
            no-numero
          />
          <!-- Carteles de validación de campo -->
          <field-messages name="nombre" show="$dirty">
            <div slot="required" class="alert alert-danger mt-1">
              Campo requerido
            </div>
            <div slot="no-espacios" class="alert alert-danger mt-1">
              No se permiten espacios intermedios en este campo
            </div>
             <div slot="no-numero" class="alert alert-danger mt-1">
              No se permiten numeros
            </div>
            <div slot="minlength" class="alert alert-danger mt-1">
              Se deben ingresar como mínimo {{ nombreLengthMin }} caracteres
            </div>
            <div
              v-if="formData.nombre.length == nombreLengthMax"
              class="alert alert-danger mt-1"
            >
              Máximo de caracteres ({{ nombreLengthMax }}) alcanzados
            </div>
          </field-messages>
        </validate>
        <br />
        <validate tag="div">
          <label for="edad"><i>Edad</i></label>
          <input
            type="number"
            id="edad"
            name="edad"
            class="form-control my-3"
            autocomplete="off"
            v-model.trim="formData.edad"
            required
            :min="edadMin"
            :max="edadMax"
            no-espacios
          />
          <!-- Carteles de validación de campo -->
          <field-messages name="edad" show="$dirty">
            <div slot="required" class="alert alert-danger mt-1">
              Campo requerido
            </div>
            <div slot="no-espacios" class="alert alert-danger mt-1">
              No se permiten espacios intermedios en este campo
            </div>
            <div slot="min" class="alert alert-danger mt-1">
              Edad minima {{ edadMin }} años
            </div>
            <div slot="max" class="alert alert-danger mt-1">
              Edad maxima {{ edadMax }} años
            </div>
          </field-messages>
        </validate>

        <br />

        <validate tag="div">
          <label for="edad"><i>Email</i></label>
          <input
            type="email"
            id="email"
            name="email"
            class="form-control my-3"
            autocomplete="off"
            v-model.trim="formData.email"
            required
            no-espacios
          />
          <!-- Carteles de validación de campo -->
          <field-messages name="email" show="$dirty">
            <div slot="required" class="alert alert-danger mt-1">
              Campo requerido
            </div>
            <div slot="no-espacios" class="alert alert-danger mt-1">
              No se permiten espacios intermedios en este campo
            </div>
            <div slot="email" class="alert alert-danger mt-1">
              Email no válido
            </div>
          </field-messages>
        </validate>

        <button
          class="btn btn-success my-4"
          :disabled="formState.$invalid"
          type="submit"
        >
          Enviar
        </button>
      </vue-form>
      <hr />

      <tabla :posts="post" />
    </div>
  </section>
</template>

<script lang="js">

import tabla from './tabla.vue'

  export default  {
    name: 'src-components-formulario',
   components: {
      tabla
   },
  props: [],
  data () {
    return {
      formData : this.getInicialData(),
      formState: {},
      nombreLengthMin : 5,
      nombreLengthMax: 15,
      edadMin: 18,
      edadMax: 120,
       post : []

    }
  },
  computed: {


  },
  mounted () {

  },
  methods: {

    getInicialData() {
      return {
        nombre: '',
        edad: '',
        email: '',
       }
    },

    enviar() {
      console.log({...this.formData})

      this.post.push(this.formData)
      this.formData = this.getInicialData()
      this.formState._reset()

    }
  }
}
</script>

<style scoped lang="css">
.src-components-formulario {
  background-size: cover;
  background-color: rgba(56, 61, 47, 0.87);
 
}

.titulo {
  padding-top: 10px;
  text-align: center;
}
hr {
  color: rgb(255, 255, 255);
}
.container {
  padding-top: 10px;
  padding-bottom: 5%;
}
h2 {
  color: rgb(255, 255, 255);
}
form {
  color: white;
}
</style>
