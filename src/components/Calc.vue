<template>
  <div class="calc-container">
    <div class="value-container">
      <h2>{{ value }}</h2>
    </div>
    <div class="calc-wrapper">
      <button>C</button>
      <button @click="Add()">+/-</button>
      <button>%</button>
      <button class="button-color-swap">÷</button>
    </div>
    <div class="calc-wrapper">
      <input type="button" @click="SetValue(7)" value="7" />
      <input type="button" @click="SetValue(8)" value="8" />
      <input type="button" @click="SetValue(9)" value="9" />
      <button class="button-color-swap">x</button>
    </div>
    <div class="calc-wrapper">
      <input type="button" @click="SetValue(4)" value="4" />
      <input type="button" @click="SetValue(5)" value="5" />
      <input type="button" @click="SetValue(6)" value="6" />
      <button class="button-color-swap">-</button>
    </div>
    <div class="calc-wrapper">
      <input type="button" @click="SetValue(1)" value="1" />
      <input type="button" @click="SetValue(2)" value="2" />
      <input type="button" @click="SetValue(3)" value="3" />
      <button class="button-color-swap" @click="operator = '+'">+</button>
    </div>
    <div class="calc-wrapper">
      <button class="zero-button-size" @click="SetValue(0)" value="0">0</button>
      <button>,</button>
      <button @click="results()" class="button-color-swap">=</button>
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
      operator: "",
    };
  },
  methods: {
    SetValue(enterdValue) {
      if (this.operator != "") {
        this.secondValue += enterdValue;
        this.value = this.secondValue;
      } else {
        this.firstValue += enterdValue;
        this.value = this.firstValue;
      }
    },
  },
  computed: {
    results() {
      switch (this.operator) {
        case "+":
          this.value = parseInt(this.firstValue) + parseInt(this.secondValue);
          break;
      }
    },
  },
};
</script>
<style scoped>
.calc-container {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  width: 100%;
  row-gap: 10px;
}
.calc-wrapper {
  display: flex;
  flex-wrap: wrap;
  gap: 10px;
}

button {
  font-size: 20px;
  font-weight: bold;
  width: 60px;
  height: 60px;
  border-radius: 60px;
  background: grey;
  border: none;
}

input[type="button"] {
  font-size: 20px;
  font-weight: bold;
  width: 60px;
  height: 60px;
  border-radius: 60px;
  background: grey;
  border: none;
}
button:hover {
  background: lightblue;
}
.zero-button-size {
  width: 130px;
}
.button-color-swap {
  font-size: 25px;
  background: orange;
}
.value-container {
  font-size: 20px;
  width: 55%;
  text-align: right;
}
</style>
