<template>
  <div class="calculator">
    <div @click="clear" class="btn clean">ON/CE</div>
    <div class="score">{{current || '0'}}</div>
    <div class="btn">OFF</div>
    <div @click="sqrt" class="btn">√</div>
    <div class="btn">%</div>
    <div @click="division" class="btn">÷</div>
    <div @click="append('7')" class="btn">7</div>
    <div @click="append('8')" class="btn">8</div>
    <div @click="append('9')" class="btn">9</div>
    <div @click="multiplication" class="btn">x</div>
    <div @click="append('4')" class="btn">4</div>
    <div @click="append('5')" class="btn">5</div>
    <div @click="append('6')" class="btn">6</div>
    <div value="-" @click="minus" class="btn">-</div>
    <div @click="append('1')" class="btn">1</div>
    <div @click="append('2')" class="btn">2</div>
    <div @click="append('3')" class="btn">3</div>
    <div @click="plus" class="btn plus">+</div>
    <div @click="append('0')" class="btn">0</div>
    <div @click="dot" class="btn">.</div>
    <div @click="equally" class="btn">=</div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      previous: null,
      current: '',
      operator: null,
      operatorClicked: false
    }
  },
  methods: {
    clear() {
      this.current = '';
    },
    sqrt() {
      if(parseFloat(this.current) >= 0)
        this.current = Math.sqrt(parseFloat(this.current))
    },
    // percent() {
    //   this.current = `${parseFloat(this.current) / 100}`
    // },
    append(number) {
      if (this.operatorClicked) {
        this.current = '';
        this.operatorClicked = false;
      }
      this.current = `${this.current}${number}`;
    },
    dot() {
      if (this.current.indexOf('.') === -1) {
        this.append('.');
      }
    },
    setPrevious() {
      this.previous = this.current;
      this.operatorClicked = true;
    },
    division() {
      this.operator = (a, b) => b / a;
      this.setPrevious();
    },
    multiplication() {
      this.operator = (a, b) => a * b;
      this.setPrevious();
    },
    minus() {
      this.operator = (a, b) => b - a;
      this.setPrevious();
    },
    plus() {
      this.operator = (a, b) => a + b;
      this.setPrevious();
    },
    equally() {
      this.current = `${this.operator(
        parseFloat(this.current),
        parseFloat(this.previous)
      )}`;
    }
  }
}
</script>

<style scoped>
.calculator {
  display: grid;
  grid-template-colums: repeat(4, 1fr);
  grid-auto-rows: mimax(50px, auto);
  margin: 0 auto;
  max-width: 450px;
  font-size: 2em;
}

.clean {
  background-color: #4DBED7;
}

.score {
  grid-column: 2 / 5;
  background-color: #D2D2D2;
}

.plus {
  grid-column: 4 / 5;
  grid-row: 5 / 7;
  background-color: #4DBED7;
}

.btn {
  border: 1px solid #eee;
  user-select: none;
  cursor:pointer;
}
.btn:active {
  transform: scale(0.95);
}
</style>
