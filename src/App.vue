<template>
  <div id="app">
    <!-- <img alt="Vue logo" src="./assets/logo.png" /> -->
    <!-- <HelloWorld msg="Welcome to Your Vue.js App" /> -->
    <Index />
  </div>
</template>

<script>
// import HelloWorld from "./pages/HelloWorld.vue";
import Index from "./pages/Index.vue";

export default {
  name: "App",
  components: {
    // HelloWorld,
    Index
  }
};
</script>

<style lang="less">
body {
  padding: 0;
  margin: 0;
  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    height: 100%;
  }
}
</style>
