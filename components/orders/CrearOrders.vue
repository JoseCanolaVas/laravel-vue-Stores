<template>

  <div>
    <v-card>
      <v-alert dense color="indigo" icon="mdi-plus">Crear Orden</v-alert>
      <v-card-text>
        <template>
          <v-form ref="formCrear">

            <v-row>
              <v-col cols="12" sm="12" md="12">
                <v-select :items="states" menu-props="auto" label="Stores" hide-details prepend-icon="mdi-cart-outline"
                  single-line></v-select>
              </v-col>

              <v-col cols="12" sm="12" md="12">
                <v-text-field label="Numero Ordenes" type="number"></v-text-field>
              </v-col>

              <v-col cols="12" sm="12" md="12">
                <v-text-field label="Proveedor"></v-text-field>
              </v-col>

            </v-row>
          </v-form>
        </template>

      </v-card-text>
      <v-card-actions>
        <v-btn dark color="red darken-4" small @click="cerrarModal()">Cerrar</v-btn>
        <v-btn dark color="teal" small>Guardar</v-btn>
      </v-card-actions>
    </v-card>
  </div>
</template>

<script>
export default {
  props: {
    value: Boolean,
  },



  methods: {
    cerrarModal() {
      this.$emit("close-modal");
    }
  }



}
</script>
