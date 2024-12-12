<template>

  <div>
    <ListarProducts :headers="headersProducts" :items="products" :loading="loading.products" :products="products" />
  </div>
</template>
<script>
import ListarProducts from '../../components/products/ListarProducts.vue'
export default {
  components: {
    ListarProducts,
  },

  data() {
    return {
      loading: {
        products: false,
      },

      products: [],
      buscar: "",
      headersProducts: [
        {
          text: "Name",
          value: "name",
          align: "center",
        },
        {
          text: "Description",
          value: "description",
          align: "center",
        },
        {
          text: "Supplier",
          value: "supplier",
          align: "center",
        },
        {
          text: "Price",
          value: "price",
          align: "center",
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
    this.listar();
  },

  methods: {
    async listar() {
      try {
        this.loading.products = true;
        const response = await this.$axios.get("/products/listar");
        this.products = response.data;
      } catch (error) {
        this.$toast.error("No se pueden listar los productos");
      } finally {
        this.loading.products = false;
      }
    }

  }


}
</script>
