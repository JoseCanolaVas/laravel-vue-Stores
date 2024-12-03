<template>
  <v-card>
    <v-alert>
      <b>Crear</b>
    </v-alert>
    <v-card-text>
      <template>
        <v-form ref="formCrear" max-width="600px">
          <v-row dense>
            <v-col cols="12" sm="3" md="4">
              <v-text-field label="Name" outlined></v-text-field>
            </v-col>
            <v-col cols="12" sm="3" md="4">
              <v-text-field label="Owner" outlined></v-text-field>
            </v-col>
            <v-col cols="12" sm="3" md="4">
              <v-text-field label="Location" outlined></v-text-field>
            </v-col>
          </v-row>
        </v-form>

      </template>
      <v-card-actions>
        <v-btn color="error"><v-icon>mdi-close</v-icon> Cerrar</v-btn>
        <v-btn color="success"><v-icon>mdi-plus</v-icon>Crear</v-btn>
      </v-card-actions>
    </v-card-text>


  </v-card>


</template>

<script>
export default {

}
</script>
