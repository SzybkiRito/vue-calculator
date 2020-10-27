<template>
  <Calculator />
</template>

<script>
import Calculator from "./components/Calculator.vue";

export default {
  name: "App",
  components: {
    Calculator
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
  background-color: #fce043;
  background-image: linear-gradient(315deg, #fce043 0%, #fb7ba2 74%);
  background-repeat: no-repeat;
  background-attachment: fixed;
  margin: 0;
}
</style>
