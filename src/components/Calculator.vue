<template>
  <div class="calculator">
    <!-- Display !-->
    <div class="display">          
      <div class="operation">{{operationString}}</div>
      <div>{{currentNumber || '0'}}</div>
    </div>

    <!-- Buttons !-->
    <button v-on:click="clear" class="btne">C</button> 
    <button v-on:click="sign" class="btne">+/-</button> 
    <button  class="btne">%</button> 
    <button v-on:click="divide" class="btne operator">÷</button> 
    <button v-on:click="appendNumber('7')" class="btne">7</button> 
    <button v-on:click="appendNumber('8')" class="btne">8</button> 
    <button v-on:click="appendNumber('9')" class="btne">9</button> 
    <button v-on:click="times" class="btne operator">x</button> 
    <button v-on:click="appendNumber('4')" class="btne">4</button> 
    <button v-on:click="appendNumber('5')" class="btne">5</button> 
    <button v-on:click="appendNumber('6')" class="btne">6</button> 
    <button v-on:click="minus" class="btne operator">-</button>
    <button v-on:click="appendNumber('1')" class="btne">1</button> 
    <button v-on:click="appendNumber('2')" class="btne">2</button> 
    <button v-on:click="appendNumber('3')" class="btne">3</button> 
    <button v-on:click="plus" class="btne operator">+</button>
    <button v-on:click="appendNumber('0')" class="btne zero">0</button> 
    <button v-on:click="dot" class="btne">.</button>
    <button v-on:click="equal" class="btne operator">=</button>    
  </div>
</template>

<script>
export default {
  data(){
    return{
      operationString: '',
      previousNumber: null,
      currentNumber: '0', 
      operator: null,
      isOperating: false,
      resetString: false,
      resetOperation: false,
      afterDotLimit: 0,
      numberLimit: 0      
    }
  },

  methods: {
    clear() {
      this.currentNumber = '0';
      this.operationString = '';
      this.numberLimit = 0;
      this.afterDotLimit = 0;
    },

    sign() {    
      if(this.currentNumber != '0')
        this.currentNumber = this.currentNumber.charAt(0) === '-' ? 
        this.currentNumber.slice(1) : `${'-'}${this.currentNumber}`;      
    },

    percent() {
      //TODO
    },

    dot() {
      if(this.currentNumber.indexOf('.') === -1)
        if(this.currentNumber == '0')
          this.appendNumber('0.');
        else
          this.appendNumber('.');
    },

    appendString(string) {
      if(this.resetString){
        this.operationString = '';
        this.resetString = false;
      } 

      this.operationString = `${this.operationString}${string}`;
    },

    appendNumber(number) {
      if(this.currentNumber == '0' && number != '.')
        this.currentNumber = '';

      if(this.isOperating) {
        this.currentNumber = '';
        this.isOperating = false;
      }

      if(this.resetOperation) {
        this.currentNumber = '';
        this.resetOperation = false;
      }
      
      //if the number is less then 8
      if(this.numberLimit < 8 && this.currentNumber.indexOf('.') === -1) {        
        this.currentNumber = `${this.currentNumber}${number}`;
        this.numberLimit++;             
      }//if the number is less then 8 and number is dot
      else if(this.numberLimit == 8 && number == '.') {
        this.currentNumber = `${this.currentNumber}${number}`;
      }//if the number has dot
      else if(this.afterDotLimit < 4 && this.currentNumber.indexOf('.') !== -1) {
        this.currentNumber = `${this.currentNumber}${number}`;
        this.afterDotLimit++
      }
    },    

    setPreviousNumber() {
      this.previousNumber = this.currentNumber;
      this.isOperating = true;
      this.numberLimit = 0;
      this.afterDotLimit = 0;      
    },

    divide() {
      this.operator = (x, y) => x / y;
      this.setPreviousNumber();
      this.appendString(`${this.currentNumber} ÷ `);
    },

    times() {
      this.operator = (x, y) => x * y;
      this.setPreviousNumber();
      this.appendString(`${this.currentNumber} x `);
    },

    minus() { 
      this.operator = (x, y) => x - y;
      this.setPreviousNumber();
      this.appendString(`${this.currentNumber} - `);
    },

    plus() {      
      this.operator = (x, y) => x + y;
      this.setPreviousNumber();
      this.appendString(`${this.currentNumber} + `);
    },

    equal() {
      this.operationString = `${this.operationString}${this.currentNumber} = `
      this.currentNumber = `${this.operator(
        parseFloat(this.previousNumber),
        parseFloat(this.currentNumber)
      )}`;
      
      this.verifyNumber()

      this.previousNumber = null;
      this.resetString = true;
      this.resetOperation = true;
      this.numberLimit = 0;
      this.afterDotLimit = 0;
    },

    verifyNumber() {
      //if the number has no dot
      if(this.currentNumber.indexOf('.') === -1){
        if(this.currentNumber.length > 8)
          this.currentNumber = "Too Big";        
      }
      else {
        if(this.currentNumber.length > 13)
          this.currentNumber = "Too Big";
        else {
          let dotPoint = this.currentNumber.indexOf('.');
          let afterDot = 0;
  
          for(let i = dotPoint; i < this.currentNumber.length; i++)
            afterDot +=  1;
  
          //if have less numbe then 4 after the dot
          if(afterDot > 4)
            this.currentNumber = parseFloat(this.currentNumber).toFixed(4);        
        }
      }      
    }
  }
}
</script>


<style scoped>
  .calculator {
    background-color: rgb(20, 0, 73);
    margin: 0 auto;
    padding: 6px;
    display: grid;
    width: 300px;
    font-size: 35px;    
    grid-template-columns: repeat(4, 1fr);
    grid-auto-rows: minmax(50px, auto);
  }

  .display {
    margin: 6px;    
    background-color: rgb(221, 221, 221);
    text-align: right;
    color: black;
    grid-column: 1 / 5;
  }  

  .operation {      
    font-size: 18px;
  }

  .btne {
    margin: 6px;
    box-shadow:inset 0px 1px 0px 0px #54a3f7;
    background:linear-gradient(to bottom, #007dc1 5%, #0061a7 100%);
    background-color:#007dc1;
    border-radius:3px;
    border:1px solid #124d77;
    display:inline-block;
    cursor:pointer;
    color:#ffffff;
    font-family:Arial;
    font-size:25px;
    text-decoration:none;
    text-shadow:0px 1px 0px #154682;    
  }

  .btne:hover {
    background:linear-gradient(to bottom, #0061a7 5%, #007dc1 100%);
    background-color:#0061a7;
  }
  .btne:active {
    position:relative;
    top:1px;
  }

  .operator {    
    color: black;
  }

  .zero {
    grid-column: 1 / 3;
  }
</style>
