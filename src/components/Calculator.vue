<template>
  <div class="calculator">
    <!-- Display !-->
    <div class="display">      
      <div class="operation">{{operationString}}</div>
      <div>{{currentNumber || '0'}}</div>
    </div>

    <!-- Buttons !-->
    <div @click="clear" class="btn">C</div>
    <div @click="sign" class="btn">+/-</div>
    <div class="btn">%</div>
    <div @click="divide" class="btn operator">/</div>
    <div @click="appendNumber('7')" class="btn">7</div>
    <div @click="appendNumber('8')" class="btn">8</div>
    <div @click="appendNumber('9')" class="btn">9</div>
    <div @click="times" class="btn operator">x</div>
    <div @click="appendNumber('4')" class="btn">4</div>
    <div @click="appendNumber('5')" class="btn">5</div>
    <div @click="appendNumber('6')" class="btn">6</div>
    <div @click="minus" class="btn operator">-</div>
    <div @click="appendNumber('1')" class="btn">1</div>
    <div @click="appendNumber('2')" class="btn">2</div>
    <div @click="appendNumber('3')" class="btn">3</div>
    <div @click="plus" class="btn operator">+</div>
    <div @click="appendNumber('0')" class="btn zero">0</div>
    <div @click="dot" class="btn">.</div>
    <div @click="equal" class="btn operator">=</div>
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
      resetOperation: false          
    }
  },

  methods: {
    clear() {
      this.currentNumber = '0';
      this.operationString = '';
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

      this.currentNumber = `${this.currentNumber}${number}`;      
    },    

    setPreviousNumber() {
      this.previousNumber = this.currentNumber;
      this.isOperating = true;
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
      this.previousNumber = null;
      this.resetString = true;
      this.resetOperation = true;
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
    color: rgb(96, 210, 255);
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
    font-size: 20px;
  }

  .btn {
    margin: 6px;
    border: 1px solid rgb(13, 0, 128);
    background-color: rgb(3, 71, 199);
  }

  .operator {
    background-color:rgb(25, 149, 207);
    color: black;
  }

  .zero {
    grid-column: 1 / 3;
  }
</style>
