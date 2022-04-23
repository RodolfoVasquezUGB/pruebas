<template>
<div>
    <b-table striped hover :items="lenguajes" :fields="fields">
      <!-- editar -->
      <template v-slot:cell(edit)="data">
        <b-button
          v-b-modal.modal-1
          variant="btn btn-primary"
          @click="editLenguaje(data.item)">
          Edit
        </b-button>
      </template>

      <!-- eliminar -->
      <template v-slot:cell(delete)="data">
        <b-button variant="btn btn-danger" @click="deleteLenguaje(data.item)">
          Delete
        </b-button>
      </template>
    </b-table>

    <!-- editar datos -->
    <div>
      <b-modal id="modal-1" title="BootstrapVue">
        <b-form>
          <b-form-group id="input-group-1" label="Nombre:" label-for="input-1">
            <b-form-input
              id="input-1"
              v-model="selectedLenguaje.nombre"
              placeholder="Nombre del lenguaje de programacion"
              required
            ></b-form-input>
          </b-form-group>

          <b-form-group id="input-group-2" label="Informacion:" label-for="input-2">
            <b-form-input
              id="input-2"
              v-model="selectedLenguaje.informacion"
              placeholder="Informacion del lenguaje de programacion"
              required
            ></b-form-input>
          </b-form-group>

          <b-form-group id="input-group-3" label="Creador:" label-for="input-3">
            <b-form-input
              id="input-3"
              v-model="selectedLenguaje.creador"
              placeholder="Creador del lenguaje de programacion"
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
              v-model="selectedLenguaje.fecha"
              placeholder="Ingrese la fecha que se creo el lenguaje de programacion"
              required
            ></b-form-input>
          </b-form-group>


          <span style="color: red">{{ msg }}</span>
          <br />
          <hr />
          <b-button variant="primary" v-on:click="updateLenguaje()"
            >Actualizar</b-button
          >
        </b-form>
      </b-modal>
    </div>
  </div>
</template>
<script>
import axios from "axios";
export default {
  name: "LenguajeCom",
  data() {
    return {
      lenguajes: [],
      selectedLenguaje: [],
      fields: [
        {
          key: "id",
          soportable: true,
        },
        {
          key: "nombre",
          soportable: true,
        },
        {
          key: "informacion",
          soportable: true,
        },
        {
          key: "creador",
          soportable: true,
        },
        {
          key: "fecha",
          soportable: true,
        },
        {
          key: "Edit",
          label: "Editar",
        },
        {
          key: "Delete",
          label: "Borrar",
        },
      ],
      msg: "",
    };
  },
  created() {
    // api
    axios
      .get("http://localhost:8000/api/lenguajes")
      .then((response) => {
        this.lenguajes = response.data.data;
      })
      .catch((e) => {
        this.errors.push(e);
      });
  },
   methods: {
    deleteLenguaje(lenguaje) {
      axios
        .delete("http://localhost:8000/api/pelicula/" + lenguaje.id)
        .then(() => {
          this.lenguajes = this.lenguajes.filter((p) => p.id !== lenguaje.id);
        })
        .catch((e) => {
          this.errors.push(e);
        });
    },
    editLenguaje(lenguaje) {
      this.selectedLenguaje = lenguaje;
    },
    updateLenguaje() {
      axios.put("http://localhost:8000/api/lenguajes", this.selectedLenguaje);
      if (
        this.selectedLenguaje.nombre != "" &&
        this.selectedLenguaje.informacion != "" &&
        this.selectedLenguaje.creador != "" &&
        this.selectedLenguaje.fecha != "" 
      ) {
        this.msg = "Datos registrados con éxito";
      } else {
        this.msg = "Se necesita todos los campos rellenos";
      }
    },
  },
};
</script>