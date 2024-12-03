<template>
  <div>
    <ListarStores :headers ="headersStores" :items="stores" :loading="loading.stores" :stores="stores" />
  </div>
</template>

<script>
import ListarStores from '../../components/stores/ListarStores.vue';
export default {
  components: {
    ListarStores,
  },

  data() {
    return {
      loading: {
        stores: false,
      },

      stores: [],
      buscar: "",
      headersStores: [
        {
          text: "name",
          value: "name",
          align: "center",
        },
        {
          text: "owner",
          value: "owner",
          align: "center",
        },
        {
          text: "location",
          value: "location",
          align: "center",
        },
        {
          text: "Acciones",
          value: "acciones",
          align: "center",
          sortable: false,
        }
      ]
    }
  },

  mounted(){
    this.ListarStores();
  },

  methods: {
    async ListarStores(){
      try {
       this.loading.stores = true;
       const response = await this.$axios.get("/stores/listarStores");
       this.$toast.success("¡ Stores Listado !");
       this.stores = response.data;
      } catch (error) {
       this.$toast.error("Error al listar las Stores");
      } finally{
        this.loading.stores = false;
      }
    }
  }

}

</script>
