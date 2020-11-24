<template>
  <div id="app">
    <myGames/>
  </div>
</template>

<script>
import myGames from './view/myGames.vue'

export default {
  name: 'App',
  components: {
    myGames
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #353535;
}
</style>
