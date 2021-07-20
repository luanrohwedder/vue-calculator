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
    font-family: 'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif;
    background-color: blanchedalmond;
    margin: 0 auto;
    width: 350px;
    margin-top: 20px;
    border: 5px solid #1C6EA4;
    padding-top: 10px;
    padding-bottom: 10px;
    font-size: 20px;
  }
  .adviceText {   
    padding-left: 10px; 
    text-align: left;
  }
</style>