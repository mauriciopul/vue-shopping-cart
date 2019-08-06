<template>
  <div>
    <div>
      <form>
        <input v-model="codigoProducto" placeholder="Codigo del producto" />
        <input v-model="nombreProducto" placeholder="Nombre del producto" />
        <input v-model="precioProducto" placeholder="Precio del producto" />
      </form>
      <button v-on:click="postProducts()">Crear</button>
    </div>
    <table>
      <tbody>
        <tr v-for="product_post in products" :key="product_post.codigoProducto">
          <td>{{product_post.codigoProducto}}</td>
          <td>{{product_post.nombreProducto}}</td>
          <td>{{product_post.precioProducto}}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      products: "",
      codigoProducto: "",
      nombreProducto: "",
      precioProducto: 2
    };
  },

  mounted() {
    this.getProducs();
  },

  methods: {
    getProducs() {
      axios
        .get("http://localhost:3000/products/")
        .then(response => {
          this.products = response.data.products;
          console.log("Data de response", response.data.products);
        })
        .catch(error => {
          console.log(error);
        });
    },
    postProducts() {
      const params = {
        codigoProducto: this.codigoProducto,
        nombreProducto: this.nombreProducto,
        precioProducto: this.precioProducto
      };
      axios
        .post("http://localhost:3000/products/", params)
        .then(response => {
          this.codigoProducto = "";
          this.nombreProducto = "";
          this.precioProducto;
        })
        .catch(error => {
          console.log(error);
        });
      this.getProducs();
    }
  }
};
</script>

<style>
</style>