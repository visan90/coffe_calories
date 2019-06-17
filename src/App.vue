<template>
  <div id="app">
    <CoffeChoose/>
  </div>
</template>

<script>
import CoffeChoose from './components/CoffeChoose.vue'

export default {
  name: 'app',
  components: {
    CoffeChoose
  }
}
</script>

<style>
#app {
  font-family: 'Raleway', sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
