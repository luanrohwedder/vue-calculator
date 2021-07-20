<template>
  <div id="app">
    <Calculator/>
    <Advice/>
  </div>
</template>

<script>
import Calculator from './components/Calculator.vue'
import Advice from './components/Advice.vue'

export default {
  name: 'App',
  components: {
    Calculator,    
    Advice
  }
}
</script>

<style>

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;  
  margin-top: 60px;  
}
</style>
