<template>

  <div>
    <h1>listado de ordenes</h1>
    <br>
    <v-row dense>
      <v-col cols="12" sm="10" md="10">
        <v-text-field label="Buscar" v-model="buscar"></v-text-field>
      </v-col>

      <v-col cols="12" sm="2" md="2">
        <v-btn block color="success" @click="CrearOrdersA()">
          <v-icon>mdi-plus</v-icon> Crear Orden
        </v-btn>
      </v-col>

    </v-row>

    <v-data-table :headers="headers" :items="items" :loading="loading" loading-text="Cargando ... Por favor espere."
      no-data-text="Sin datos para Mostrar">

      <template v-slot:[`item.acciones`]="{ item }">
        <v-tooltip top>
          <template v-slot:activator="{ on, attrs }">
            <v-icon color="warning" small class="mr-2" v-bind="attrs" v-on="on" @click="abrirModalEditar(item)">
              mdi-pencil
            </v-icon>
          </template>
          <span>Editar</span>

          <v-tooltip>
            <template v-slot:action="{ on, attrs }">
              <v-icon color="" v-bind="attrs" v-on="on">
                mdi-toggle-switch-off-outline
              </v-icon>
            </template>
          </v-tooltip>
        </v-tooltip>



      </template>
    </v-data-table>

    <v-dialog v-model="formCrear" max-width="900px" persistent>
      <CrearOrders @close-modal="cerrarModal"/>
    </v-dialog>

  </div>
</template>

<script>
import CrearOrders from '../../components/orders/CrearOrders.vue';
export default {

  components: {
    CrearOrders,
  },

  props: {
    headers: Array,
    items: Array,
    search: String,
    loading: Boolean,

  },

  data(){
    return{
      formCrear: false,
    }
  },

  methods: {
    abrirModalEditar() {
      this.formEditarOrden = true;
    },

    cerrarModal(){
      this.formCrear = false;
    },

    CrearOrdersA(){
      this.formCrear = true;
    }
  }



}

</script>
