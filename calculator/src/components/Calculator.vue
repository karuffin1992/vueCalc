<template>
  <div class="calculator">
    <div class="display">{{ current }}</div>
    <div @click="clear" class="operator button">CE</div>
    <div @click="sign" class="operator button">+/-</div>
    <div @click="percent" class="operator button">%</div>
    <div @click="divide" class="operator button">/</div>
    <div @click="number('7')" class="button">7</div>
    <div @click="number('8')" class="button">8</div>
    <div @click="number('9')" class="button">9</div>
    <div @click="multiply" class="operator button">X</div>
    <div @click="number('4')" class="button">4</div>
    <div @click="number('5')" class="button">5</div>
    <div @click="number('6')" class="button">6</div>
    <div @click="subtract" class="operator button">-</div>
    <div @click="number('1')" class="button">1</div>
    <div @click="number('2')" class="button">2</div>
    <div @click="number('3')" class="button">3</div>
    <div @click="add" class="operator button">+</div>
    <div @click="number('0')" class="zero button">0</div>
    <div @click="decimal" class="button">.</div>
    <div @click="equals" class="operator button">=</div>
  </div>
</template>

<script>
export default {
  name: "Calculator",
  data() {
    return {
      current: '',
      previous: null,
      operator: null,
      operatorClicked: false
    };
  },
  methods: {
    clear() {
      // Clear current value
      this.current = '';
    },
    number(number) {
      // Need to check if an operator has been clicked already
      // If so, reset
      if(this.operatorClicked){
        this.current = '';
        this.operatorClicked = false;
      }
      this.current = `${this.current}${number}`;
    },
    sign() {
      // Setting negative/positive status
      this.current = this.current.charAt(0) === '-' ?
        this.current.slice(1) : `-${this.current}`;
    },
    percent() {
      // Getting percentage of number
      this.current = `${parseFloat(this.current) / 100}`;
    },
    decimal() {
      // Only one decimal should exist in a number
      this.current = this.current.indexOf('.') > 0 ?
        this.current : `${this.current}.`
    },
    setPrevious() {
      // Used in math operations (below)
      // Need to set previous number in calc to current number
      // Then set operatorClicked flag
      this.previous = this.current;
      this.operatorClicked = true;
    },
    divide() {
      this.operator = (a,b) => a / b;
      this.setPrevious();
    },
    multiply() {
      this.operator = (a,b) => a * b;
      this.setPrevious();
    },
    subtract() {
      this.operator = (a,b) => a - b;
      this.setPrevious();
    },
    add() {
      this.operator = (a,b) => a + b;
      this.setPrevious();
    },
    equals() {
      // Uses operator function with values
      this.current = `${this.operator(parseFloat(this.previous), parseFloat(this.current))}`;
      this.previous = null;
    }
  }
};
</script>

<style scoped>
  .calculator {
    margin: 100px auto;
    width: 400px;
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    grid-auto-rows: minmax(40px,auto);
  }

  .zero {
    grid-column: 1 / 3;
  }

  .display{
    grid-column: 1 / 5;
    grid-row: 1;
    background-color: #4d4e4f;
    color: white;
  }

  .display, .button {
    text-align: center;
    justify-content: center;
    border: 1px solid black;
    font-size: 30px;
  }

  .operator {
    background-color: orange;
    color: white;
  }
</style>
