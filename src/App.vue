<template>
  <div id="app">
    <Converter
            v-bind:imgsrc="imgsrc"
            v-bind:units="units"/>
  </div>
</template>

<script>
  import Converter from "./components/Converter";

  export default {
    name: 'App',
    data(){
      return{
        imgsrc : "/images/numbers.jpg",
        units: {
          feet: "Футы",
          arshin: "Аршины",
          metres: "Метры",
          verst: "Версты"
        }
      }
    },
    components: {
      Converter
    }
  }
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
</style>
