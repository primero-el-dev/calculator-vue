<template>
  <div>
    <NumberDisplay :content="currentNumber" />
    <div>
      <NumberButton :onClick="appendNumber" :content="7" />
      <NumberButton :onClick="appendNumber" :content="8" />
      <NumberButton :onClick="appendNumber" :content="9" />
      <ActionButton :onClick="arithmeticAction(divide)" :content="'/'" />
    </div>
    <div>
      <NumberButton :onClick="appendNumber" :content="4" />
      <NumberButton :onClick="appendNumber" :content="5" />
      <NumberButton :onClick="appendNumber" :content="6" />
      <ActionButton :onClick="arithmeticAction(multiply)" :content="'*'" />
    </div>
    <div>
      <NumberButton :onClick="appendNumber" :content="1" />
      <NumberButton :onClick="appendNumber" :content="2" />
      <NumberButton :onClick="appendNumber" :content="3" />
      <ActionButton :onClick="arithmeticAction(subtract)" :content="'-'" />
    </div>
    <div>
      <NumberButton :onClick="appendNumber" :content="0" />
      <ActionButton :onClick="appendDot" :content="'.'" />
      <ActionButton :onClick="arithmeticAction(modulo)" :content="'mod'" />
      <ActionButton :onClick="arithmeticAction(add)" :content="'+'" />
    </div>
    <div>
      <ActionButton :onClick="calculate" :content="'='" />
      <ActionButton :onClick="clear" :content="'C'" />
      <ActionButton :onClick="clearAll" :content="'AC'" />
    </div>
  </div>
</template>

<script>
import NumberDisplay from './components/NumberDisplay'
import NumberButton from './components/NumberButton'
import ActionButton from './components/ActionButton'

export default {
  name: 'App',
  components: {
    NumberDisplay,
    NumberButton,
    ActionButton
  },
  data() {
    return {
      previousNumber: null,
      currentNumber: '0',
      displayedResult: false,
      currentOperation: null,
      clear: () => {
        this.currentNumber = '0'
      },
      clearAll: () => {
        this.previousNumber = null
        this.currentNumber = '0'
        this.displayedResult = false
        this.currentOperation = null
      },
      calculate: () => {
        let result = this.currentOperation(this.previousNumber, this.currentNumber)
        this.previousNumber = this.currentNumber
        this.currentNumber = result
        this.displayedResult = true
      },
      appendNumber: (number) => {
        if (this.currentNumber == '0' || this.displayedResult) {
          this.currentNumber = number
          this.displayedResult = false
        } else {
          this.currentNumber += '' + number
        }
      },
      appendDot: () => {
        if (!this.currentNumber.includes('.')) {
          this.currentNumber += '.'
        }
      },
      add: (a, b) => parseFloat(a) + parseFloat(b),
      subtract: (a, b) => parseFloat(a) - parseFloat(b),
      multiply: (a, b) => parseFloat(a) * parseFloat(b),
      divide: (a, b) => parseFloat(a) / parseFloat(b),
      modulo: (a, b) => parseFloat(a) % parseFloat(b),
      arithmeticAction: func => () => {
        if (this.previousNumber && this.currentOperation) {
          this.calculate()
        } else {
          this.previousNumber = this.currentNumber
          this.currentNumber = '0'
        }
        this.currentOperation = func
      }
    }
  }
}
</script>

<style>
*,
*::before,
*::after {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  font-size: 1.5rem;
}

.calculator--btn {
  width: 4rem;
  height: 2rem;
  font-size: 1.5rem;
}
</style>
