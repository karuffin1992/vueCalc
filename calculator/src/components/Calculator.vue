<template>
  <div class="calculator">
    <div class="display">{{ display }}</div>
    <div @click="clear" class="button">CE</div>
    <div @click="sign" class="button">+/-</div>
    <div @click="percent" class="button">%</div>
    <div class="button">/</div>
    <div @click="number('7')" class="button">7</div>
    <div @click="number('8')" class="button">8</div>
    <div @click="number('9')" class="button">9</div>
    <div class="button">X</div>
    <div @click="number('4')" class="button">4</div>
    <div @click="number('5')" class="button">5</div>
    <div @click="number('6')" class="button">6</div>
    <div class="button">-</div>
    <div @click="number('1')" class="button">1</div>
    <div @click="number('2')" class="button">2</div>
    <div @click="number('3')" class="button">3</div>
    <div class="button">+</div>
    <div @click="number('0')" class="zero button">0</div>
    <div @click="decimal" class="button">.</div>
    <div class="button">=</div>
  </div>
</template>

<script>
export default {
  name: "Calculator",
  data() {
    return {
      display: ''
    };
  },
  methods: {
    clear() {
      this.display = '';
    },
    number(number) {
      this.display = `${this.display}${number}`;
    },
    sign() {
      this.display = this.display.charAt(0) === '-' ?
        this.display.slice(1) : `-${this.display}`;
    },
    percent() {
      this.display = `${parseFloat(this.display) / 100}`;
    },
    decimal() {
      this.display = this.display.indexOf('.') > 0 ?
        this.display : `${this.display}.`
    }
  }
};
</script>

<style scoped>
  .calculator {
    margin: 0 auto;
    width: 400px;
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    grid-auto-rows: minmax(50px,auto)
  }

  .zero {
    grid-column: 1 / 3;
  }

  .display{
    grid-column: 1 / 5;
    grid-row: 1;
  }

  .display, .button {
    text-align: center;
    justify-content: center;
    border: 1px solid black;
    font-size: 30px;
  }
</style>
