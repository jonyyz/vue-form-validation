<template>
  <div id="app">
    <person-form />
  </div>
</template>

<script>
import PersonForm from "./components/PersonForm.vue";

export default {
  name: "App",
  components: {
    PersonForm
  }
};
</script>

<style>
* {
  box-sizing: border-box;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
</style>
