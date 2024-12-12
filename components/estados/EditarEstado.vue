<template>
  <v-card>
    <v-alert dense color="indigo darken-4" icon="mdi-pencil">
      <b>Editar Estado v-card {{ estadoSeleccionado?.id }}</b>
    </v-alert>
    <v-card-text>
      <template>
        <v-form ref="editarForm">

        <v-row dense>
          <v-col cols="12" sm="12" md="12">
            <v-text-field label="Nombre"></v-text-field>
          </v-col>
          <v-col cols="12" sm="12" md="12">
            <v-text-field label="Descripcion"></v-text-field>
          </v-col>
        </v-row>

        </v-form>

      </template>
    </v-card-text>
    <v-card-actions>
      <v-btn color="red darken-4" small @click="cerrarModal">Cerrar</v-btn>
      <v-btn color="lime darken-3" small @click="editarEstado">Editar</v-btn>

    </v-card-actions>
  </v-card>
</template>

<script>
export default {
  props: {
    value: Boolean,

    estadoSeleccionado:{
      type: Boolean,

    }
  },

  data(){
    return{
      editarForm
    }
  },

  methods:{
    cerrarModal(){
      this.$emit('cerrar')
    }
  }

}
</script>
