<template>
  <v-card>
    <v-alert dense text color="primary" icon="mdi-pencil">
      <b>Editar Product Seleccionado {{ productoSeleccionado?.id }}</b>
    </v-alert>

      <v-card-text>
        <v-template>
        <v-form ref="editarForm">
          <v-row dense>
            <v-col cols="12" sm="12" md="12">
              <v-text-field label="Name" dense outlined></v-text-field>
            </v-col>
            <v-col cols="12" sm="12" md="12">
              <v-text-field label="Description" dense outlined>
              </v-text-field>
            </v-col>
            <v-col cols="12" sm="12" md="12">
              <v-text-field label="Supplier" dense outlined></v-text-field>
            </v-col>
            <v-col cols="12" sm="12" md="12">
              <v-text-field label="Price" type="number" dense outlined></v-text-field>
            </v-col>

          </v-row>
        </v-form>
      </v-template>
      </v-card-text>

    <v-card-actions>
      <v-spacer></v-spacer>
      <v-btn small dark color="red" @click="cerrarEditar()">Cerrar</v-btn>
      <v-btn small dark color="success" @click="actualizar">actualizar</v-btn>
    </v-card-actions>
  </v-card>
</template>

<script>
export default {
  props: {
    formModalEditar:{
      type: Boolean,
      default: false,
    },

    productoSeleccionado:{
      type: Boolean,
    },

    data() {
      return{
        editarForm:{
          name: "",
          description: "",
          supplier: "",
          price: "",
        },

        rules:{
          obligatorio: (v) => !!v || "Este campo es obligatorio",
          minimo: (v) => v.length >= 5 || " Este campo debe tener minimo 5 Caracteres"
        },

      };

    },

    methods:{

      cerrarEditar(){
        this.$emit('cerrar')
      }

    }

    // productoSeleccionado: {
    //   typeo: Object,
    //   default: () => ({}),
    // }

  }

}
</script>
