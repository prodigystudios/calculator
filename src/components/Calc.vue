<template>
  <div class="calc-container">
    <div class="value-container calc-wrapper">
      <h2>{{ value }}</h2>
    </div>
    <div class="calc-wrapper">
      <button @click="Clear()">C</button>
      <button @click="SetValue('-')">+/-</button>
      <button @click="SelectedOperator('%')">%</button>
      <button class="button-color-swap" @click="SelectedOperator('/')">÷</button>
    </div>
    <div class="calc-wrapper">
      <input type="button" @click="SetValue(7)" value="7" />
      <input type="button" @click="SetValue(8)" value="8" />
      <input type="button" @click="SetValue(9)" value="9" />
      <button class="button-color-swap" @click="SelectedOperator('*')">x</button>
    </div>
    <div class="calc-wrapper">
      <input type="button" @click="SetValue(4)" value="4" />
      <input type="button" @click="SetValue(5)" value="5" />
      <input type="button" @click="SetValue(6)" value="6" />
      <button class="button-color-swap" @click="SelectedOperator('-')">-</button>
    </div>
    <div class="calc-wrapper">
      <input type="button" @click="SetValue(1)" value="1" />
      <input type="button" @click="SetValue(2)" value="2" />
      <input type="button" @click="SetValue(3)" value="3" />
      <button type="button" class="button-color-swap" @click="SelectedOperator('+')">
        +
      </button>
    </div>
    <div class="calc-wrapper">
      <input class="zero-button-size" type="button" @click="SetValue(0)" value="0" />
      <input type="button" @click="SetValue('.')" value="," />
      <button @click="Results()" class="button-color-swap" value="=">=</button>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      value: "0",
      firstValue: "",
      secondValue: "",
      lastCalculated: "",
      operator: "+",
      calcStarted: false,
    };
  },
  methods: {
    SetValue(enterdValue) {
      if (!this.calcStarted) {
        this.value = "";
      }
      this.calcStarted = true;
      this.value += enterdValue;
    },
    SelectedOperator(selectedOperator) {
      this.operator = selectedOperator;
      this.calcStarted = false;

      if (this.firstValue == "") {
        this.firstValue = parseFloat(this.value);
        return;
      }
      if (this.firstValue != "") {
        this.Results();
      }
    },
    Results() {
      this.secondValue = parseFloat(this.value);
      switch (this.operator) {
        case "+":
          this.value = parseFloat(this.firstValue) + parseFloat(this.secondValue);
          this.secondValue = "";
          this.firstValue = this.value;
          break;
        case "-":
          this.value = parseFloat(this.firstValue) - parseFloat(this.secondValue);
          this.secondValue = "";
          this.firstValue = this.value;
          break;
        case "*":
          this.value = parseFloat(this.firstValue) * parseFloat(this.secondValue);
          this.secondValue = "";
          this.firstValue = this.value;
          break;
        case "/":
          this.value = parseFloat(this.firstValue) / parseFloat(this.secondValue);
          this.secondValue = "";
          this.firstValue = this.value;
          break;
        case "%":
          const decimalCalc = parseFloat(this.firstValue) / 100;
          this.value = decimalCalc * this.secondValue;
          this.secondValue = "";
          this.firstValue = this.value;
          break;
      }
    },
    Clear() {
      this.value = "0";
      this.firstValue = "";
      this.secondValue = "";
      this.calcStarted = false;
    },
  },
};
</script>
<style scoped>
.calc-container {
  margin-top: 10px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  width: 100%;
  row-gap: 10px;
}
.calc-wrapper {
  display: flex;
  gap: 10px;
  margin-bottom: 5px;
}

button {
  font-size: 20px;
  font-weight: bold;
  width: 80px;
  height: 80px;
  border-radius: 60px;
  background: grey;
  border: none;
}

input[type="button"] {
  font-size: 20px;
  font-weight: bold;
  width: 80px;
  height: 80px;
  border-radius: 200px;
  background: rgb(31, 30, 30);
  border: none;
  color: rgb(255, 255, 255);
}
input[type="button"]:hover {
  background: lightblue;
}
button {
  color: rgb(19, 3, 3);
}
button:hover {
  background: lightblue;
}
button:focus {
  background: rgb(255, 254, 254);
  color: orange;
}
.zero-button-size {
  width: 160px !important;
}
.button-color-swap {
  font-size: 25px;
  background: orange;
}
.calc-wrapper h2 {
  width: 100%;
}
.value-container {
  font-size: 25px;
  position: relative;
  left: 135px;
}
</style>
