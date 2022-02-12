<template>
  <div class="Advice">
      <span>This calculator have some limitations:</span>
      <div class="adviceText">
        <br>
        <span>- 8 numbers before dot <br> - 4 numbers after dot <br></span>
        <span>- Don't support number greater than 8 numbers <br> - Four operations: / + - x</span>
      </div>
  </div>
</template>

<script>
export default {

}
</script>

<style>
  .Advice {
    margin: 0 auto;
    width: 350px;
    margin-top: 20px;
    border-top: 2px solid #424242;
    border-bottom: 2px solid #424242;
    padding-top: 10px;
    padding-bottom: 10px;
    font-size: 20px;
  }
  .adviceText {   
    padding-left: 10px; 
    text-align: left;
  }
</style>