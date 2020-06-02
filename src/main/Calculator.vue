<template>
  <div class="calculator">
    <Display :value= "displayValue" />
    <Button label="AC" triple @onClick="clearMemory" />
    <Button label="/" operation @onClick="setOperation" />
    <Button label="7" @onClick="addDigt" />
    <Button label="8" @onClick="addDigt" />
    <Button label="9" @onClick="addDigt" />
    <Button label="*" operation @onClick="setOperation" />
    <Button label="4" @onClick="addDigt" />
    <Button label="5" @onClick="addDigt" />
    <Button label="6" @onClick="addDigt" />
    <Button label="-" operation @onClick="setOperation" />
    <Button label="1" @onClick="addDigt" />
    <Button label="2" @onClick="addDigt" />
    <Button label="3" @onClick="addDigt" />
    <Button label="+" operation @onClick="setOperation" />
    <Button label="0" double @onClick="addDigt" />
    <Button label="." @onClick="addDigt" />
    <Button label="=" operation @onClick="setOperation" />
  </div>
</template>

<script>
import Display from "../components/Display";
import Button from "../components/Button";

export default {
  components: { Button, Display },
  data: function() {
    return {
      displayValue: "0",
      clearDisplay: false,
      operation: null,
      values: [0, 0],
      current: 0
    };
  },
  methods: {
    clearMemory() {
      Object.assign(this.$data, this.$options.data());
    },
    setOperation(operation) {
      if (this.current === 0) {
        this.operation = operation;
        this.current = 1;
        this.clearDisplay = true;
      } else {
        const equals = operation === "=";
        const currentOperation = this.operation;
        try {
          this.values[0] = eval(
            `${this.values[0]} ${currentOperation} ${this.values[1]}`
          );
        } catch (e) {
          this.$emit("onError", e);
        }
        this.values[1] = 0;
        this.displayValue = this.values[0];
        this.operation = equals ? null : operation;
        this.current = equals ? 0 : 1;
        this.clearDisplay = !equals;
      }
    },
    addDigt(n) {
        if (n === "." && this.displayValue.includes(".")) {
                return
            }
            const clearDisplay = this.displayValue === "0"
                || this.clearDisplay
            const currentValue = clearDisplay ? "" : this.displayValue
            const displayValue = currentValue + n
            this.displayValue = displayValue
            this.clearDisplay = false
            this.values[this.current] = displayValue

    }
  }
};
</script>

<style>
.calculator {
  height: 320px;
  width: 235px;
  border-radius: 5px;
  overflow: hidden; /*Determinando que não pode passar do tamanho especicado*/

  display: grid;
  grid-template-columns: repeat(
    4,
    25%
  ); /*Criando 4 colunas que usam 25% do tamanho da calculadora*/
  grid-template-rows: 1fr 48px 48px 48px 48px 48px; /*1fr usa o resto de fragmentos deixado, os 48pxs são o tamanho das linhas da calculadora*/
}
</style>