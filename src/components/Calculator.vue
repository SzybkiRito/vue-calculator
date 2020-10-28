<template>
  <div class="container">
    <div class="calculator">
      
      <div class="output" style="color: pink; font-weight: 2px;">
        <span>{{ result }}</span>
        <span>{{ previousValue }} {{ operatorString }} {{ currentValue || 0}}</span>
      </div>

      <button type="submit" class="group_one" @click="percent">%</button>
      <button type="submit" class="group_two" @click="changeSign">+/-</button>
      <button type="submit" class="group_three" @click="clearCurrentValue()">C</button>
      <button type="submit" class="operator" @click="divide()">/</button>
      <button type="submit" class="group_one" @click="append('7')">7</button>
      <button type="submit" class="group_two" @click="append('8')">8</button>
      <button type="submit" class="group_three" @click="append('9')">9</button>
      <button type="submit" class="operator" @click="multiply">X</button>
      <button type="submit" class="group_one" @click="append('4')">4</button>
      <button type="submit" class="group_two" @click="append('5')">5</button>
      <button type="submit" class="group_three" @click="append('6')">6</button>
      <button type="submit" class="operator" @click="minus">-</button>
      <button type="submit" class="group_one" @click="append('1')">1</button>
      <button type="submit" class="group_two" @click="append('2')">2</button>
      <button type="submit" class="group_three" @click="append('3')">3</button>
      <button type="submit" class="operator" @click="add">+</button>
      <button type="submit" class="group_one" @click="append('0')">0</button>
      <button type="submit" class="group_two" @click="dot">.</button>
      <button type="submit" style="width: 120px; background-color: rgb(177, 31, 128);" @click="equal()">=</button>
    </div>
  </div>
</template>

<script>
import { ref } from "vue";

export default {
  name: "Calculator",
  setup() {
    let currentValue = ref("");
    let previousValue = ref("");
    let result = ref("");
    let operator = null;
    let operatorString = ref("");
    let operatorClicked = false;

    function append(number) {
      if (operatorClicked && currentValue.value == "") {
        operatorString.value = "";
      }
      if (operatorClicked) {
        currentValue.value = "";
        operatorClicked = false;
      }
      currentValue.value = `${currentValue.value}${number}`;
    }
    function setPrevious() {
      previousValue.value = currentValue.value;
      operatorClicked = true;
    }
    function divide() {
      operator = (a, b) => a / b;
      operatorString.value = "/";
      setPrevious();
    }
    function multiply() {
      operator = (a, b) => a * b;
      operatorString.value = "*";
      setPrevious();
    }
    function add() {
      operator = (a, b) => a + b;
      operatorString.value = "+";
      setPrevious();
    }
    function minus() {
      operator = (a, b) => a - b;
      operatorString.value = "-";
      setPrevious();
    }
    function percent() {
      currentValue.value = `${parseFloat(currentValue.value) / 1000}`;
    }
    function clearCurrentValue() {
      currentValue.value = "";
    }
    function changeSign() {
      currentValue.value =
        currentValue.value.charAt(0) === "-"
          ? currentValue.value.slice(1)
          : `-${currentValue.value}`;
    }
    function dot() {
      if (currentValue.value.indexOf(".") === -1) {
        append(".");
      }
    }
    function equal() {
      if(previousValue.value == "") return;
      currentValue.value = `${operator(
        parseFloat(currentValue.value),
        parseFloat(previousValue.value)
      )}`;
      previousValue.value = "";
      operatorString.value = "";
    }

    return {
      currentValue,
      previousValue,
      operator,
      operatorString,
      operatorClicked,
      result,
      // Functions down
      append,
      setPrevious,
      equal,
      divide,
      multiply,
      add,
      minus,
      percent,
      changeSign,
      dot,
      clearCurrentValue,
    };
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.container {
  display: flex;
  align-items: center;
  justify-content: center;
  flex-wrap: wrap;
  font-size: 25px;
}
.calculator {
  width: 250px;
  text-align: center;
  box-shadow: 0px 0.25px rgba(151, 151, 151, 0.25);
}
.operator {
  background-color: blueviolet;
}
.group_one {
  background-color: rgba(151, 151, 151, 0.25);
}
.group_two {
  background-color: rgba(151, 151, 151, 0.20);
}
.group_three {
  background-color: rgba(151, 151, 151, 0.15);
}
span {
  margin-right: 20px;
}
.calculator .output {
  max-width: 240px;
  height: 50px;
  text-align: right;
  padding-top: 25px;
  margin: 0 auto;
  background-color: rgb(43, 43, 43);
  color: white;
}
button {
  width: 60px;
  height: 60px;
  outline: none;
  border: none;
}
</style>
