<template>
  <div id="app">
    <Something/>
  </div>
</template>

<script>
import Something from './components/Something.vue'

export default {
  name: 'app',
  components: {
    Something
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
