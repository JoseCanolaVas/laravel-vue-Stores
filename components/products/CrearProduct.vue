<template>
  <v-card>
    <v-alert dense text color="primary" icon="mdi-plus">
      <b>Crear Product</b>
    </v-alert>
    <v-card-text>
      <template>
        <v-form ref="formModalCrear">
          <v-row dense>
            <v-col cols="12" sm="12" md="12">
              <v-text-field dense outlined label="Name" v-model="formProduct.name">

              </v-text-field>
            </v-col>
            <v-col cols="12" sm="12" md="12">
              <v-text-field dense outlined label="Description" v-model="formProduct.description">

              </v-text-field>
            </v-col>
            <v-col cols="12" sm="12" md="12">
              <v-text-field dense outlined label="Supplier" v-model="formProduct.supplier">

              </v-text-field>
            </v-col>
            <v-col cols="12" sm="12" md="12">
              <v-text-field dense outlined label="Store" v-model="formProduct.store">

              </v-text-field>
            </v-col>
            <v-col cols="12" sm="12" md="12">
              <v-text-field dense outlined label="Price" v-model="formProduct.price">
              </v-text-field>
            </v-col>
          </v-row>
        </v-form>
      </template>
    </v-card-text>
      <v-card-actions>
        <v-btn small dark color="red" @click="cerrarModal()">Salir</v-btn>
        <v-btn small dark color="success" @click="crearProduct()">Crear</v-btn>
      </v-card-actions>
  </v-card>
</template>

<script>

export default {
  props: {
    value: Boolean,
  },

  data() {
    return {
      formProduct: {
        name: "",
        description: "",
        supplier: "",
        store: "",
        price: "",
      },

      rules: {
        obligatorio: (v) => !!v || "Este campo es obligatorio",
        minimo: (v) => v.lenght >= 5 || "Ingrese minimo 5 caracteres",
      }
    }
  },
  mounted() {
    this.listar
  },

  methods: {

    cerrarModal() {
      this.$emit("cerrar");
    },

    async crearProduct(){
      try {
        this.preload = true;
        await = this.$axios.post('/')
      } catch (error) {
          this.$toast.error(error);
      }
    }

  }
}
</script>
