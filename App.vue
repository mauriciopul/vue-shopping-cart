<template>
  <div>

    <div>
      <form id="form" class="topBefore">

        <input v-model="codigoProducto" placeholder="Codigo del producto" /><br>
        <input v-model="nombreProducto" placeholder="Nombre del producto" /><br>
        <input type="number" v-model="precioProducto" placeholder="Precio del producto" /><br>        
        <button v-on:click="postProducts()" id="submit">Crear</button> <br><br> 
      
      </form>
        <form id="form" class="topBefore">
          <input v-model="codigoProducto" placeholder="Codigo del producto" /><br>
          <button v-on:click="getOneProduct(codigoProducto)">Buscar</button>
          <button v-on:click="deleteProduct()">Eliminar</button>  
        </form>
    </div>
    <table>
      <tbody>
        <h2>
          </h2>
            <tr>
            <td><h2>codigo</h2></td>
            <td><h2>Producto</h2></td>
            <td><h2>Precio</h2></td>
       
          </tr>
        
          <tr v-for="product_post in products" :key="product_post.codigoProducto">
          <td>{{product_post.codigoProducto}}</td>          
          <td>{{product_post.nombreProducto}}</td>          
          <td>{{product_post.precioProducto}}</td>
          <td>{{product_post._id}}</td>
          <!--<td><button v-on:click="removeProduct(product_post._id)">eliminar</button></td>-->
          
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
      _id: "",
      nombreProducto: "",
      precioProducto: ""
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

    getOneProduct(codigo) {
      axios
        .get("http://localhost:3000/products/codigo/" + codigo)
        .then(response => {
          console.log(response);
          if (response.data.products.length < 0) {
            alert("sin data");
            return;
          }
          this._id = response.data.products._id;
          this.codigoProducto = response.data.products.codigoProducto;
          this.nombreProducto = response.data.products.nombreProducto;
          this.precioProducto = response.data.products.precioProducto;
        });
    },

    deleteProduct() {
      let producto = this.products.filter(
        product => product.codigoProducto === this.codigoProducto
      );
      axios
        .delete("http://localhost:3000/products/" + producto[0]._id)
        .then(response => {
          this.getProducs();
        });
    }

    // removeProduct() {
    //   console.log('ingresando al metodo');
    //   debugger
    //   let producto = this.products.filter(product => product.codigoProducto === this.codigoProducto);
    //   console.log(producto[0]._id, 'producto a remover')

    //   axios
    //     .delete("http://localhost:3000/products/" + producto._id)
    //     .then(response => {
    //       this.getProducs();
    //     });
    // }
  }
};
</script>

<style>
</style>

<!--
<style>
.header {
  color: #36a0ff;
  font-size: 27px;
  padding: 10px;
}

.bigicon {
  font-size: 35px;
  color: #36a0ff;
}
</style>
-->



<!--
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
  color: #aca49c;
  font-size: 0.875em;
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
  width: 502px;

  padding: 0;
  margin: -5px 0px 0px 0px;

  font-family: "Lato", sans-serif;
  font-size: 1.2em;
  color: rgba(52, 58, 58, 0.432);

  outline: none;
  cursor: pointer;

  border: solid 1px #b3aca7;
  border-top: none;
}

#submit:hover {
  color: black;
}
</style>
-->



<!--

    <form id="form" class="topBefore">
		
		  <input id="name" type="text" placeholder="NAME">
		  <input id="email" type="text" placeholder="E-MAIL">
		  <textarea id="message" type="text" placeholder="MESSAGE"></textarea>
  <input id="submit" type="submit" value="GO!">
  
</form>
  ---------------------------------------------
    <div class="container">
    <div class="row">
        <div class="col-md-12">
            <div class="well well-sm">
                <form class="form-horizontal" method="post">
                    <fieldset>
                        <legend class="text-center header">Contact us</legend>

                        <div class="form-group">
                            <span class="col-md-1 col-md-offset-2 text-center"><i class="fa fa-user bigicon"></i></span>
                            <div class="col-md-8">
                                <input id="fname" name="name" type="text" placeholder="First Name" class="form-control">
                            </div>
                        </div>
                        <div class="form-group">
                            <span class="col-md-1 col-md-offset-2 text-center"><i class="fa fa-user bigicon"></i></span>
                            <div class="col-md-8">
                                <input id="lname" name="name" type="text" placeholder="Last Name" class="form-control">
                            </div>
                        </div>

                        <div class="form-group">
                            <span class="col-md-1 col-md-offset-2 text-center"><i class="fa fa-envelope-o bigicon"></i></span>
                            <div class="col-md-8">
                                <input id="email" name="email" type="text" placeholder="Email Address" class="form-control">
                            </div>
                        </div>

                        <div class="form-group">
                            <span class="col-md-1 col-md-offset-2 text-center"><i class="fa fa-phone-square bigicon"></i></span>
                            <div class="col-md-8">
                                <input id="phone" name="phone" type="text" placeholder="Phone" class="form-control">
                            </div>
                        </div>

                        <div class="form-group">
                            <span class="col-md-1 col-md-offset-2 text-center"><i class="fa fa-pencil-square-o bigicon"></i></span>
                            <div class="col-md-8">
                                <textarea class="form-control" id="message" name="message" placeholder="Enter your massage for us here. We will get back to you within 2 business days." rows="7"></textarea>
                            </div>
                        </div>

                        <div class="form-group">
                            <div class="col-md-12 text-center">
                                <button type="submit" class="btn btn-primary btn-lg">Submit</button>
                            </div>
                        </div>
                    </fieldset>
                </form>
            </div>
        </div>
    </div>
  </div>

    
     -->