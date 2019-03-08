<template>
  <div id="app">
    <link
      rel="stylesheet"
      href="https://use.fontawesome.com/releases/v5.2.0/css/all.css"
      integrity="sha384-hWVjflwFxL6sNzntih27bfxkr27PmbbK/iSvJ+a4+0owXq79v+lsFkW54bOGbiDQ"
      crossorigin="anonymous"
    />
    <PmHeader />
    <!-- <HelloWorld/> -->
    <router-view />
    <PmFooter />
  </div>
</template>

<script>
import PmFooter from "./components/layout/Footer";
import PmHeader from "./components/layout/Header";

export default {
  name: "App",
  data() {
    return {};
  },
  components: {
    PmFooter,
    PmHeader
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.search  {
  height: 20px;
  font-size: 5em;
}
#lista-artistas li {
  list-style: none;
}
.isActive {
  border: 2px #167bff solid;
}
#main-container {
  min-height: 100vh;
}
</style>
