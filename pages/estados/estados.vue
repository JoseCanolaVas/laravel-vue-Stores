<template>
  <div>
    <v-alert border="left" colored-border color="blue lighten-2" elevation="2" icon="mdi-information-slab-circle">
      Puedes agregar al Listado los Estado que quieras manejar dentro de los Modulos .
    </v-alert>
    <hr color="indigo">

    <ListarEstados :headers="headersEstados" :items="estados" :loading="loading.estados" :estados="estados" />

  </div>
</template>

<script>
import ListarEstados from '../../components/estados/ListarEstados.vue';
export default {
  components: {
    ListarEstados
  },

  data() {
    return {
      loading: {
        estados: true,
      },

      estados: [],
      buscar: "",
      headersEstados: [
        {
          text: "Id",
          align: "center",
          value: "id"
        },
        {
          text: "Nombre",
          align: "center",
          value: "nombre",
        },
        {
          text: "Descripcion",
          align: "center",
          value: "descripcion"
        },
        {
          text: "Acciones",
          align: "center",
          value: "acciones"
        }

      ]

    }
  },

  mounted(){
    this.ListarEstados();
  },

  methods:{

    async ListarEstados() {
      try {
        this.loading.estados = true;
        const response = await this.$axios.get('/estados/');
        this.estados = response.data;
      } catch (error) {

      } finally {
        this.loading.estados = false;
      }
    }

  }


}

</script>
