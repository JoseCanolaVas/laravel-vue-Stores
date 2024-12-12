<template>
  <div>

    <v-card>
      <v-alert dense text color="teal" icon="mdi-plus">
        <b>Crear Estado</b>
      </v-alert>
      <v-card-text>
        <template>
          <v-form ref="crearForm">
            <v-row dense>
              <v-col cols="12" sm="12" md="12">
                <v-text-field v-model="crearForm.nombre" label="Nombre *" :rules="[rules.obligatorio]"></v-text-field>
              </v-col>
              <v-col cols="12" sm="12" md="12">
                <v-textarea label="Descripcion *" v-model="crearForm.descripcion" dense outlined
                  :rules="[rules.obligatorio, rules.minimo]"></v-textarea>
              </v-col>
            </v-row>
          </v-form>
        </template>
      </v-card-text>

      <v-card-actions>
        <v-btn color="red darken-4" small @click="cerrarModal">Cerrar</v-btn>
        <v-btn color="teal" small @click="crearEstado()">Crear</v-btn>
      </v-card-actions>
    </v-card>

    <!-- Preload -->
    <v-dialog v-model="preload" persistent width="300">
      <v-card color="indigo darken-2" dark>
        <v-card-text>
          Cargando Solicitud !
          <v-progress-linear indeterminate color="white" class="mb-0"></v-progress-linear>
        </v-card-text>
      </v-card>
    </v-dialog>
  </div>
</template>

<script>

export default {
  props: {
    value: Boolean
  },

  data() {
    return {
      preload: false,
      crearForm: {
        nombre: "",
        descripcion: "",
      },
      rules: {
        obligatorio: (v) => !!v || "Este campo es obligatorio",
        minimo: v => v &&
          v.length >= 10 || "Este campo debe tener al menos 10 caracteres ",
      },
    }
  },

  mounted() {

  },

  methods: {


    cerrarModal() {
      this.limpiarFormulario();
      this.$emit("cerrar");
    },



    async crearEstado() {

      if (!this.$refs.crearForm.validate()) {
        return;
      }

      try {
        this.preload = true
        await this.$axios.post('/estados/crearEstado', this.crearForm);
        this.$toast.success("se ha creado el Estado");
        this.cerrarModal();
        this.$emit("recargarEstados");
      } catch (error) {
        console.log(error)
        this.$toast.error("Ha ocurrido un error al crear el Estado");
      } finally {
        this.preload = false;
      }
    },

    limpiarFormulario() {
      this.crearForm = {
        nombre: "",
        descripcion: "",
      }

      this.$refs.crearForm.resetValidation();
    },

  },

};
</script>
