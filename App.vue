<template>
  <div>
    <div>
      <form>
        <input v-model="codigoProducto" placeholder="Codigo del producto" />
        <input v-model="nombreProducto" placeholder="Nombre del producto" />
        <input type="number" v-model="precioProducto" placeholder="Precio del producto" />
        <p>Precio: {{precioProducto}}</p>
      </form>
      <button v-on:click="postProducts()">Crear</button>
    </div>
    <table>
      <tbody>
        <h2>
          </h2>
            <tr>
            <td><h2>id</h2></td>
            <td><h2>Producto</h2></td>
            <td><h2>Precio</h2></td>
       
          </tr>
        
          <tr v-for="product_post in products" :key="product_post.codigoProducto">
          <td><h4>{{product_post.codigoProducto}}</h4></td>          
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
      precioProducto: ""
    };
  },

  mounted() {
    this.getProducs();
    //this.created();
    //axios.create();
  },

  methods: {
    getProducs() {
      axios
        .get("http://localhost:3000/products/")
        .then(response => {
          this.products = response.data.products;
        })
        .catch(error => {
          console.log(error);
        });
    },
    postProducts() {
      const params = {
        codigoProducto: this.codigoProducto,
        nombreProducto: this.nombreProducto,
        precioProducto: parseInt(this.precioProducto)
      };

      axios
        .post("http://localhost:3000/products/", params)
        .then(response => {
          this.codigoProducto = "";
          this.nombreProducto = "";
          this.precioProducto;
          this.getProducs();
        })
        .catch(error => {
          console.log(error);
        });
    },
    getOneProduct(codigoProducto) {
      axios
        .get("http://localhost:3000/products/${codigoProducto}")
        .then(response => {
          console.log(response.data);
          this.codigoProducto = response.data.codigoProducto;
          this.nombreProducto = response.data.nombreProducto;
          this.precioProducto = response.data.precioProducto;
        });
    }
  }
};
</script>

<style>
</style>