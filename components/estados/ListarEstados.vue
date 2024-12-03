<template>
    <div>
    <h1>Estados</h1>
    <v-row dense>
      <v-col cols="12" sm="10" md="10">
        <v-text-field label="Buscar" v-model="buscar"></v-text-field>
      </v-col>
      <v-col cols="12" sm="2" md="2">
        <v-btn dark color="red" icon="md-plus-circle">Crear Estado</v-btn>
      </v-col>
    </v-row>
    <v-data-table :headers="headers" :items="items" dense :search="search" :loading="loading" disable-pagination
    loading-text="Cargando ... Por favor espere." no-data-text="Sin datos para Mostrar"></v-data-table>


    </div>
</template>
<script>

export default{
  props: {
    headers: Array,
    items: Array,
    search: String,
    loading: Boolean,
  },



}

</script>
