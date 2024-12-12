<template>
  <div>
    <h1>Listado Productos</h1>
    <br>
    <v-row dense>
      <v-col cols="12" sm="10" md="10">
        <v-text-field label="Buscar" v-model="buscar"></v-text-field>
      </v-col>
      <v-col cols="12" sm="2" md="2">
        <v-btn color="success" block small dark @click="abrirModalCrear()">Crear
          <v-icon small right>mdi-plus-circle-outline</v-icon>
        </v-btn>
      </v-col>
    </v-row>
    <v-data-table :headers="headers" :items="items" dense :search="search" :loading="loading" disable-pagination
      loading-text="Cargando ... Por favor espere." no-data-text="Sin datos para Mostrar">

      <template v-slot:[`item.estado`]="{ item }">
        <v-chip :color="getColor(item.estado)" dark small>
          {{ item.estado }}
        </v-chip>
      </template>

      <template v-slot:[`item.acciones`]="{ item }">
        <v-tooltip top>
          <template v-slot:activator="{ on, attrs }">
            <v-icon color="warning" small class="mr-2" v-bind="attrs" v-on="on" @click="abrirModalEditar(item)">
              mdi-pencil
            </v-icon>
          </template>
          <span>Editar</span>
        </v-tooltip>

        <v-tooltip top>
          <template v-slot:activator="{ on, attrs }">
            <v-icon :color="getColor(item.estado)" small v-on="on" v-bind="attrs" @click="cambiarEstado(item)">
              mdi-toggle-switch
            </v-icon>
          </template>
          <span>Cambiar Estado</span>
        </v-tooltip>
      </template>
    </v-data-table>

    <v-dialog v-model="formModalCrear" max-width="800px" persistent>
      <CrearProduct @recargarDatos="recargarDatos" @cerrar="cerrarModal" />
    </v-dialog>


    <v-dialog v-model="formModalEditar" persistent max-width="800px">
      <EditarProduct @recargarDatos="recargarDatos" :productoSeleccionado="productoSeleccionado"
        @cerrar="cerrarModal" />
    </v-dialog>



  </div>
</template>

<script>
import EditarProduct from '../../components/products/EditarProduct.vue'
import CrearProduct from './CrearProduct.vue';
export default {
  props: {
    headers: Array,
    items: Array,
    search: String,
    loading: Boolean,
  },

  components: {
    EditarProduct,
    CrearProduct
  },


  data() {
    return {
      formModalEditar: false,
      formModalCrear: false,
      productoSeleccionado: {},
      preload: false,

    };
  },

  methods: {

    abrirModalCrear() {
      this.formModalCrear = true;
    },

    abrirModalEditar(item) {
      this.formModalEditar = true;
      this.productoSeleccionado = item;
    },

    async CrearProduct() {
      try {
        this.setPreload(true);
        await this.$axios.post("products/crear")
      } catch (error) {

      }
    },


    cerrarModal() {
      this.formModalCrear = false;
      this.formModalEditar = false;
    },

    getColor(estado){
      return estado === 'activo' ? 'green' : 'red';
    },

    cambiarEstado(){

    }



  }
};
</script>
