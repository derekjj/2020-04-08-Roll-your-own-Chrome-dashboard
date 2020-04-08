<template lang="pug">
  #app
    Calculator
</template>

<script>
import Calculator from "./components/Calculator.vue";

export default {
  name: "App",
  components: {
    Calculator
  },
  data() {
    return {};
  },
  created() {
    fetch(`https://source.unsplash.com/1600x900/?beach`).then(response => {
      this.backgroundImage = response.url;
      document.body.style.backgroundColor = "white";
      document.body.style.backgroundImage = "url('" + response.url + "')";
    });
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

body {
  min-width: 300px;
}
</style>
