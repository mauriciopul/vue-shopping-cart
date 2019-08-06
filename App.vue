<template>
<div>
  <h1>{{car}}</h1>
  <table>
    <body>
      <tr>
        <td>Hola1</td>
        <td>Hola2</td>
        <td>Hola3</td>
      </tr>
    </body>
  </table>
</div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      car: "Hola mundo!!!"
    };
  },
  mounted() {
    console.log("hola mundo mounted");
  }
};
</script>

<style>
</style>
