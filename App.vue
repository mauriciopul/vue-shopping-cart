<template>
  <div>

    <div>
      <form id="form" class="topBefore">
        <input v-model="codigoProducto" placeholder="Codigo del producto que desea ingresar" />
        <input v-model="nombreProducto" placeholder="Nombre del producto que desea ingresar" />
        <input type="number" v-model="precioProducto" placeholder="Precio del producto que desea ingresar" />
        <button v-on:click="postProducts()" id="submit">Crear</button>       
      </form>

      <form id="form" class="topBefore">
        <input v-model="codProdElim" placeholder="Codigo del producto que desea eliminar" />
        <button v-on:click="deleteProduct()" id="submit">Eliminar</button>  
        
      </form>        
    </div>

    <form id="form2" class="topBefore">
      <table>
        <tr>
          <th colspan="3"><h3>Código</h3></th>
          <th><h3>Producto</h3></th>
          <th ><h3>Precio</h3></th>       
        </tr>
        
        <tr v-for="product_post in products" :key="product_post.codigoProducto">
          <td colspan="3">{{product_post.codigoProducto}}</td>          
          <td >{{product_post.nombreProducto}}</td>          
          <td >{{product_post.precioProducto}}</td>
        </tr>

      </table>
    </form>

  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      products: "",
      codigoProducto: "",
      _id: "",
      nombreProducto: "",
      precioProducto: "",
      codProdElim:""
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
        })
        .catch(error => {
          console.log(error);
        });
    },

    getOneProduct(codigo) {
      
      axios
        .get("http://localhost:3000/products/")
        .then(response => {
          this.products = response.data.products;
        })
        .catch(error => {
          console.log(error, "error......");
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
          this._id = "";
          this.nombreProducto = "";
          this.precioProducto;
          this.getProducs();
        })
        .catch(error => {
          console.log(error);
          alert("debe ingresar datos");
        });
    },

    deleteProduct() {
      
      let producto = this.products.filter(
        product => product.codigoProducto === this.codProdElim
      );
      console.log('eliminar');
      axios
        .delete("http://localhost:3000/products/" + producto[0]._id)
        .then(response => {
          this.getProducs();
        });
    }
  }
};
</script>

<style >
@import url(https://fonts.googleapis.com/css?family=Lato:100,300,400);

input::-webkit-input-placeholder,
textarea::-webkit-input-placeholder {
  color: #aca49c;
  font-size: 0.875em;
}

input:focus::-webkit-input-placeholder,
textarea:focus::-webkit-input-placeholder {
  color: #bbb5af;
}

input::-moz-placeholder,
textarea::-moz-placeholder {
  color: #aca49c;
  font-size: 0.875em;
}

input:focus::-moz-placeholder,
textarea:focus::-moz-placeholder {
  color: #bbb5af;
}

input::placeholder,
textarea::placeholder {
  color: darkslategrey;
  font-size: 1em;
}

input:focus::placeholder,
textarea::focus:placeholder {
  color: #bbb5af;
}

input::-ms-placeholder,
textarea::-ms-placeholder {
  color: #aca49c;
  font-size: 0.875em;
}

input:focus::-ms-placeholder,
textarea:focus::-ms-placeholder {
  color: #bbb5af;
}

/* on hover placeholder */

input:hover::-webkit-input-placeholder,
textarea:hover::-webkit-input-placeholder {
  color: #e2dedb;
  font-size: 0.875em;
}

input:hover:focus::-webkit-input-placeholder,
textarea:hover:focus::-webkit-input-placeholder {
  color: #cbc6c1;
}

input:hover::-moz-placeholder,
textarea:hover::-moz-placeholder {
  color: #e2dedb;
  font-size: 0.875em;
}

input:hover:focus::-moz-placeholder,
textarea:hover:focus::-moz-placeholder {
  color: #cbc6c1;
}

input:hover::placeholder,
textarea:hover::placeholder {
  color: #e2dedb;
  font-size: 0.875em;
}

input:hover:focus::placeholder,
textarea:hover:focus::placeholder {
  color: #cbc6c1;
}

input:hover::placeholder,
textarea:hover::placeholder {
  color: #e2dedb;
  font-size: 0.875em;
}

input:hover:focus::-ms-placeholder,
textarea:hover::focus:-ms-placeholder {
  color: #cbc6c1;
}

body {
  font-family: "Lato", sans-serif;
  background: #e2dedb;
  color: #b3aca7;
}

header {
  position: relative;
  margin: 100px 0 25px 0;
  font-size: 2.3em;
  text-align: center;
  letter-spacing: 7px;
}

#form {
  position: relative;
  width: 500px;
  margin: 50px auto 100px auto;
}
#form2 {
  position: relative;
  width: 700px;
  margin: 50px auto 100px auto;
}

input {
  font-family: "Lato", sans-serif;
  font-size: 0.875em;
  width: 470px;
  height: 50px;
  padding: 0px 15px 0px 15px;

  background: transparent;
  outline: none;
  color: #726659;

  border: solid 1px #b3aca7;
  border-bottom: none;

  transition: all 0.3s ease-in-out;
  -webkit-transition: all 0.3s ease-in-out;
  -moz-transition: all 0.3s ease-in-out;
  -ms-transition: all 0.3s ease-in-out;
}

input:hover {
  background: #b3aca7;
  color: #e2dedb;
}

textarea {
  width: 470px;
  max-width: 470px;
  height: 110px;
  max-height: 110px;
  padding: 15px;

  background: transparent;
  outline: none;

  color: #726659;
  font-family: "Lato", sans-serif;
  font-size: 0.875em;

  border: solid 1px #b3aca7;

  transition: all 0.3s ease-in-out;
  -webkit-transition: all 0.3s ease-in-out;
  -moz-transition: all 0.3s ease-in-out;
  -ms-transition: all 0.3s ease-in-out;
}

textarea:hover {
  background: #b3aca7;
  color: #e2dedb;
}

#submit {
  background: #cbc6c1;
  width: 502px;

  padding: 0;
  margin: -5px 0px 0px 0px;
  height: 60px;

  font-family: "Lato", sans-serif;
  font-size: 1.2em;
  color: white;

  outline: none;
  cursor: pointer;

  border: solid 1px #b3aca7;
  border-top: none;
}

#submit:hover {
  background: #b3aca7;
  color: black;
}



table {
  font-family: "Lato", sans-serif;
  font-size: 1em;
  width: 100%;
  color: darkslategrey;
  
  border: 1px solid #b3aca7;

  
}
th,
td {
  width: 15%;
  text-align:  left;
  vertical-align: top;
  border: 1px solid #b3aca7;
  border-collapse: collapse;
  padding: 0.3em;
  caption-side: bottom;
  
}
caption {
  padding: 0.3em;
  color: #fff;
  background: #000;
}
th {
  width: 65%;
  background: #cbc6c1;
  text-align:  center;
}
</style>


