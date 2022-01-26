<template>
  <button id="start" class="mt-2 btn-lg btn-dark" @click="CallDb()">Start</button>
  <div v-if="domande.length>0">
    <div class="d-flex mt-3 justify-content-center">
      <Card :domande="this.domande.slice(0,29)"/>
    </div>
  </div>
</template>

<script>
import "bootstrap/dist/css/bootstrap.css";
import "bootstrap/dist/js/bootstrap.min.js";
import Card from "./components/Card.vue"
export default {
  name: "App",
  components: {
    Card
  },
  data() {
    return {
      domande: [],
    };
  },
  methods: {
    CallDb() {
      const axios = require("axios");
      axios
        .get("http://localhost:3000/data")
        .then((response) => (this.domande = response.data));
      this.HideButton()
    },
    HideButton()
    {
      document.getElementById("start").style.display="none"
    }
  },
};
//resoconto
//domanda sbagliate
//capitolo
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
}
</style>
