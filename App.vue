<template>
<div>
  <table>
    <body>
      <tr v-for="new_post in news" v-bind:key="new_post.id">
        <td>{{new_post.id}}</td>
        <td>{{new_post.title}}</td>
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
      news: ""
    };
  },

  mounted() {
    console.log("hola mundo mounted");
    this.getNews();
  },

  methods: {
    getNews() {
      axios.get("https://jsonplaceholder.typicode.com/posts").then(response => {
        this.news = response.data;
        console.log("Data de response", response);
      });
    }
  }
};
</script>

<style>
</style>
