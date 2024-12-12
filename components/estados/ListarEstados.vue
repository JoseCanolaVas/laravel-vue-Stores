<template>
  <div>
    <h1>Estados</h1>
    <v-row dense>
      <v-col cols="12" sm="10" md="10">
        <v-text-field label="Buscar" v-model="search"></v-text-field>
      </v-col>
      <v-col cols="12" sm="2" md="1">
        <v-btn dark color="success" small @click="CrearEstado()"><v-icon>mdi-plus</v-icon> Crear Estado</v-btn>
      </v-col>
    </v-row>
    <v-data-table :headers="headers" :items="items" dense :search="search" :loading="loading" disable-pagination
      loading-text="Cargando ... Por favor espere." no-data-text="Sin datos para Mostrar">

      <template v-slot:[`item.acciones`]="{ item }">
        <v-tooltip top>
          <template v-slot:activator="{ on, attrs }">
            <v-icon color="warning" small class="mr-2" v-bind="attrs" v-on="on" @click="editarEstado(item)">
              mdi-pencil
            </v-icon>
          </template>
          <span>Editar</span>
        </v-tooltip>

        <v-tooltip top>
          <template v-slot:activator="{ on, attrs }">
            <v-icon color="red"  v-bind="attrs" v-on="on">mdi-delete</v-icon>
          </template>
          <span>Eliminar</span>
        </v-tooltip>
      </template>

    </v-data-table>

    <v-dialog v-model="crearModal" max-width="700px" persistent>
      <CrearEstado @cerrar="cerrarModal" @recargarEstados="onRecargarDatos" />
    </v-dialog>

    <v-dialog v-model="editarModal" max-width="700px" persistent>
      <EditarEstado @cerrar="cerrarModal" :estadoSeleccionado="estadoSeleccionado" @recargarDatos="onRecargarDatos" />
    </v-dialog>

  </div>
</template>
<script>

import CrearEstado from './CrearEstado.vue';
import EditarEstado from './EditarEstado.vue';
export default {

  components: {
    CrearEstado,
    EditarEstado
  },

  props: {
    headers: Array,
    items: Array,
    search: String,
    loading: Boolean,
  },

  data() {
    return {
      crearModal: false,
      editarModal: false,
    }
  },

  methods: {
    CrearEstado() {
      this.crearModal = true;
    },

    editarEstado(item) {
      this.editarModal = true;
      this.estadoSeleccionado = item;
    },

    cerrarModal() {
      this.crearModal = false;
    },

    onRecargarDatos() {
      this.$emit('recargarDatos');
    }

  }

}

</script>
