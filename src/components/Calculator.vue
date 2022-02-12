<template>
  <div>
    <div>
      <Display class="mini" mini :value="miniDisplay"/>            
    </div>

    <div class="calculator">
    
    <Display :value="displayValue"/>    

    <Button label="C" double @onClick="clear"/>
    <Button label="+/-" @onClick="addSign"/>
    <Button label="/" operation @onClick="addOperation"/>
    <Button label="7" @onClick="addNumber" />
    <Button label="8" @onClick="addNumber"/>
    <Button label="9" @onClick="addNumber"/>
    <Button label="*" operation @onClick="addOperation"/>
    <Button label="4" @onClick="addNumber"/>
    <Button label="5" @onClick="addNumber"/>
    <Button label="6" @onClick="addNumber"/>
    <Button label="-" operation @onClick="addOperation"/>
    <Button label="1" @onClick="addNumber"/>
    <Button label="2" @onClick="addNumber"/>
    <Button label="3" @onClick="addNumber"/>
    <Button label="+" operation @onClick="addOperation"/>
    <Button label="0" double @onClick="addNumber"/>
    <Button label="." @onClick="addNumber"/>
    <Button label="=" operation @onClick="addOperation"/>     
  </div>
  </div>
</template>

<script>
import Button from "./Button.vue"
import Display from "./Display.vue"

export default {
  components: {
    Button, Display
  },

  data(){
    return{
      miniDisplay: "",
      displayValue: "0",
      clearDisplay: false,
      op: null,
      values: [0,0],
      current: 0
    }
  },

  methods: {    
    clear() {
      Object.assign(this.$data, this.$options.data())
    },

    addOperation(op) {
      if(this.current === 0) {
        this.op = op
        this.current = 1
        this.clearDisplay = true
        this.miniDisplay = this.displayValue + " " + this.op
      }
      else {
        const equal = op === "="
        const currentOp = this.op
        const firstValue = this.values[0]
        const secondValue = this.values[1]

        try {
          this.values[0] = eval(`${this.values[0]} ${currentOp} ${this.values[1]}`)
          
          if (isNaN(this.values[0]) || !isFinite(this.values[0])) {
            this.clear();
            return;
          }
        } catch(e) {
          this.$emit('onError', e)
        }
        
        this.values[1] = 0

        this.displayValue = this.values[0]
        this.miniDisplay = equal ? firstValue + " " + this.op + " " + secondValue + " =" : this.values[0] + " " + this.op
        this.op = equal ? null : op
        this.current = equal ? 0 : 1
        this.clearDisplay = !equal
      }
    },

    addNumber(n) {
      if(n == "." && this.displayValue.includes(".")) {
        return
      }

      const clearDisplay = this.displayValue === "0" || this.clearDisplay
      const currentValue = clearDisplay ? "" : this.displayValue
      const displayValue = currentValue + n

      this.displayValue = displayValue
      this.clearDisplay = false

      if(n !== ".") {
        const i = this.current
        const newValue = parseFloat(displayValue)
        this.values[i] = newValue
      }
    },

    addSign() {      
      if(this.displayValue.includes("-")) {      
        this.displayValue = this.displayValue.substring(1)
      }
      else {
        this.displayValue = "-" + this.displayValue
      }

      const i = this.current
      const newValue = parseFloat(this.displayValue)
      this.values[i] = newValue
    }
  }  
}
</script>


<style scoped>
  .calculator {            
    display: grid;
    height: 320px;
    width: 270px;    
    overflow: hidden;
    
    grid-template-columns: repeat(4, 25%);
    grid-auto-rows: minmax(50px, auto);
  }
  
  .mini {    
    display: grid;
    overflow: hidden;    
    height: 10px;
    width: 250px;  
  }
</style>
