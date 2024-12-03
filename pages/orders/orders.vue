<template>

  <div>
    <!-- listado de ordenes -->
    <ListarOrders :headers="headersOrdenes" :items="ordenes" :loading="loading.ordenes"/>

  </div>

</template>

<script>
import ListarOrders from '../../components/orders/ListarOrders.vue';
export default {

  components: {
    ListarOrders,
  },

  data() {
    return{
      loading:{
        ordenes: false,
      },

      ordenes: [],
      buscar: "",
      headersOrdenes: [
        {
          text: "Store_Id",
          align: "center",
          value: "store_id"
        },
        {
          text: "Numero de Ordenes",
          align: "center",
          value: "numero_ordenes",
        },
        {
          text: "Proveedor",
          align: "center",
          value: "proveedor",
        },
        {
          text: "Estado",
          align: "center",
          value: "estado"
        },
        {
          text: "Acciones",
          value: "acciones",
          align: "center",
          sortable: false,
        },
      ]
    }
  },

  mounted() {
    this.listarOrders();
  },

  methods: {

   async listarOrders() {
     try {
      this.loading.ordenes = true;
      const response = await this.$axios.get("ordenes/listarOrden");
      this.ordenes = response.data;
      this.$toast.success("¡ Se han listado las Ordenes con exito !");
     } catch (error) {
      this.$toast.error("No se pueden listar las Ordenes");
     } finally{
      this.loading.ordenes = false;
     }
    }

  }
}
</script>
