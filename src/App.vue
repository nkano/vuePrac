<template>
  <div id="app">
    <HelloWorld/>
    <Cards/>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld'
import Cards from './components/Cards'

export default {
  name: 'App',
  components: {
    HelloWorld,
    Cards
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
    color: #2c3e50;
  margin: 60px;
}
</style>
