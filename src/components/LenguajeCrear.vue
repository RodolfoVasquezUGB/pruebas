<template>
  <div id="contenido" class="container">
    <h1>Formulario de Lenguajes de Programacion</h1>
    <div style="width: 40%; margin: auto">
      <b-form>
        <b-form-group id="input-group-1" label="Nombre:" label-for="input-1">
          <b-form-input
            id="input-1"
            v-model="lenguajeData.nombre"
            placeholder="Ingrese el nombre del lenguaje de programacion"
            required
          ></b-form-input>
        </b-form-group>
        <b-form-group
          id="input-group-2"
          label="Informacion:"
          label-for="input-2"
        >
          <b-form-input
            id="input-2"
            v-model="lenguajeData.informacion"
            placeholder="Ingrese la descripcion"
            required
          ></b-form-input>
        </b-form-group>

        <b-form-group
          id="input-group-3"
          label="Creador:"
          label-for="input-3"
        >
          <b-form-input
            id="input-3"
            v-model="lenguajeData.creador"
            placeholder="Nombre del Creador"
            required
          ></b-form-input>
        </b-form-group>

        <b-form-group
          id="input-group-4"
          label="Fecha:"
          label-for="input-4"
        >
          <b-form-input
            id="input-4"
            v-model="lenguajeData.fecha"
            placeholder="Ingrese la fecha"
            required
          ></b-form-input>
        </b-form-group>

        <span style="color: red">{{ msg }}</span>
        <br />
        <b-button variant="primary" v-on:click="create()">Crear</b-button>
        <b-button variant="success" v-on:click="reload()">Actualizar</b-button>
      </b-form>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "LenguajeCrear",
  data() {
    return {
      lenguajeData: {
        nombre: "",
        informacion: "",
        creador: "",
        fecha: "",
      },
      msg: "",
    };
  },
  methods: {
    create: function () {
      axios.post("http://localhost:8000/api/lenguajes", this.lenguajeData);
      if (
        this.lenguajeData.nombre != null &&
        this.lenguajeData.informacion != null &&
        this.lenguajeData.creador != null &&
        this.lenguajeData.fecha != null 
      ) {
        this.msg = "Datos registrados con éxito";
      } else {
        this.msg = "Se necesita todos los campos rellenos";
      }
    },
    reload: function () {
      this.$emit("reloadpage");
    },
  },
};
</script>

