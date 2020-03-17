<template>
  <div class="calculator">
    <div class="display">{{ current }}</div>
    <div @click="clear" class="btn">C</div>
    <div @click="sign" class="btn">+/-</div>
    <div @click="percent" class="btn">%</div>
    <div @click="divide" class="btn operator">/</div>
    <div @click="append" class="btn">7</div>
    <div @click="append" class="btn">8</div>
    <div @click="append" class="btn">9</div>
    <div @click="times" class="btn operator">x</div>
    <div @click="append" class="btn">4</div>
    <div @click="append" class="btn">5</div>
    <div @click="append" class="btn">6</div>
    <div @click="minus" class="btn operator">-</div>
    <div @click="append" class="btn">1</div>
    <div @click="append" class="btn">2</div>
    <div @click="append" class="btn">3</div>
    <div @click="add" class="btn operator">+</div>
    <div @click="append" class="btn zero">0</div>
    <div @click="dot" class="btn">.</div>
    <div @click="equal" class="btn operator">=</div>
  </div>
</template>

<script>
export default {
  name: 'Calculator',
  data() {
    return {
      previous: null,
      current: '123',
      operator: null,
      operatorClicked: false,
    }
  },
  methods: {
    clear() {
      this.current = ''
    },
    sign() {
      this.current = this.current.charAt(0) === '-' ? this.current.slice(1) : `-${this.current}`
    },
    percent() {
      this.current = `${parseFloat(this.current) / 100}`
    },
    append(n) {
      if (this.operatorClicked) {
        this.current = '';
        this.operatorClicked = false;
      }
      this.current += n.srcElement.innerText;
    },
    dot() {
      if (this.current.indexOf('.') === -1) {
        this.current += '.';
      }
    },
    setPrevious() {
      this.previous = this.current;
      this.operatorClicked = true;
      this.current = '';
    },
    divide() {
      this.operator = (a, b) => a / b;
      this.setPrevious();
    },
    add() {
      this.operator = (a, b) =>  a + b;
      this.setPrevious();
    },
    minus() {
      this.operator = (a, b) =>  a - b;
      this.setPrevious();
    },
    times() {
      this.operator = (a, b) =>  a * b;
      this.setPrevious();
    },
    equal() {
      this.current = `${this.operator(
                        parseFloat(this.current), 
                        parseFloat(this.previous)
                      )}`;
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .calculator {
    margin: 0 auto;
    width: 400px;
    font-size: 40px;
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    grid-auto-rows: minmax(50px, auto);
  }

  .display {
    /* Takes the entire first row */
    grid-column: 1 / 5;
    background-color: #333;
    color: white;
  }

  .zero {
    grid-column: 1 / 3;
  }

  .btn {
    background-color: #eee;
    border: 1px solid #999;
  }

  .operator {
    background-color: orange;

    color: white;
  }
</style>
