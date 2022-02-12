<template>
  <div id="app">
    <h1>Vue Calculator</h1>
    <Calculator/>
  </div>  
</template>

<script>
import Calculator from './components/Calculator.vue'

export default {
  name: 'App',
  components: {
    Calculator    
  }
}
</script>

<style>
@font-face {
  font-family: "Montserrat";
  src: url("./fonts/Montserrat-VariableFont_wght.ttf");
}


* {
  font-family: "Montserrat", monospace;      
}

body {
  margin: 0
}

#app {
  display: flex;
  flex-direction: column;
  height: 100vh;
  justify-content: center;
  align-items: center;
  text-align: center;
  color: rgb(211, 211, 211);
  background: linear-gradient(to right, rgb(44, 62, 80), rgb(52, 152, 219));
}
</style>
