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
  async created() {
    try {
      let res = await fetch(
        `https://source.unsplash.com/1600x900/?beach`
      ).catch();
      document.body.style.backgroundImage = (await "url('") + res.url + "')";
    } catch (err) {
      console.log("Failed to load random remote image,", err);
    }
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
