<template>
  <div class="calculator">
    <div class="display">{{ current || 0 }}</div>
    <div class="btn" @click="clear">C</div>
    <div class="btn" @click="sign">+/-</div>
    <div class="btn" @click="percent">%</div>
    <div class="btn operator" @click="divide">÷</div>
    <div class="btn" @click="append('7')">7</div>
    <div class="btn" @click="append('8')">8</div>
    <div class="btn" @click="append('9')">9</div>
    <div class="btn operator" @click="times">x</div>
    <div class="btn" @click="append('4')">4</div>
    <div class="btn" @click="append('5')">5</div>
    <div class="btn" @click="append('6')">6</div>
    <div class="btn operator" @click="minus">-</div>
    <div class="btn" @click="append('1')">1</div>
    <div class="btn" @click="append('2')">2</div>
    <div class="btn" @click="append('3')">3</div>
    <div class="btn operator" @click="plus">+</div>
    <div class="btn zero" @click="append('0')">0</div>
    <div class="btn" @click="dot">.</div>
    <div class="btn operator" @click="equal">=</div>
  </div>
</template>

<script>
export default {
  name: 'Calculator',
  data() {
    return {
      current: '',
      operator: null,
      previous: null,
      operatorClick: false
    }
  },
  methods: {
    clear() {
      this.current = ''
    },
    sign() {
      this.current = this.current.charAt(0) === '-' ?
        this.current.slice(1) : `-${this.current}`
    },
    percent() {
      this.current = `${parseFloat(this.current) / 100}`
    },
    append(number) {
      if (this.operatorClick) {
        this.current = ''
        this.operatorClick = false
      }
      this.current = `${this.current}${number}`
    },
    dot() {
      if (this.current.indexOf('.') === -1) {
        this.append('.')
      }
    },

    setPrevious() {
      this.previous = this.current
      this.operatorClick = true
    },
    divide() {
      this.operator = (a, b) => a / b
      this.setPrevious()
    },
    times() {
      this.operator = (a, b) => a * b
      this.setPrevious()
    },
    minus() {
      this.operator = (a, b) => a - b
      this.setPrevious()
    },
    plus() {
      this.operator = (a, b) => a + b
      this.setPrevious()
    },
    equal() {
      this.current = `${this.operator(parseFloat(this.current), parseFloat(this.previous))
        }`
      this.previous = null
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.calculator {
  width: 400px;
  margin: 0 auto;
  font-size: 40px;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: 50px auto;
}

.display {
  background-color: #333;
  color: white;
  grid-column: 1/5;
}

.zero {
  grid-column: 1/3;
}

.btn {
  background-color: #F2F2F2;
  border: solid 1px #999;
  cursor: pointer;
}

.operator {
  background-color: orange;
  color: white;
}
</style>
