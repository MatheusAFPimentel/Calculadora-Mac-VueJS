<template>
  <button class="button" 
  @click="$emit('onClick', label)"
  :class="{double, triple, operation}">{{ label }}</button>
</template>

<script>
export default {
  //Parametros que quero passar pro botão
  props: {
    label: {},
    operation: { type: Boolean },
    double: { type: Boolean },
    triple: { type: Boolean }
  }
};
</script>

<style>
:root {
  --bg-button: #f0f0f0; /*--bg é uma descrição de criação de classe css*/
  --border-button: solid 1px #888;
}

.button {
  font-size: 1.4em;
  background-color: var(
    --bg-button
  ); /*Referenciando a classe para ser utilizada nesse button*/
  border: none; /*Sem borda*/
  border-right: var(--border-button); /*Referenciando mais uma vez*/
  border-bottom: var(--border-button); /* Referenciando... :)*/
  outline: none; /* Tirando barrinha azul do lado*/
}

.button:active {
  background-color: rgb(161, 159, 159); /* ACTIVE - Quando o botão for ativado faça essa mudança(detalhe de mudança de cor no click)*/
}

.button.double {
    grid-column: span 2; /*Criando class para utilizar quando o numero ocupar 2 espaços na calculadora SPAN 2*/
}

.button.triple {
    grid-column: span 3; /*Criando class para utilizar quando o numero ocupar 3 espaços na calculadora SPAN 3*/
}

.button.operation {
    background-color: #fa8231; /*Especificação para quando o button for uma operação(+,-,*,/)*/
    color: #fff;
}

.button.operation:active {
    background-color: #fa8231cc; /*  ACTIVE - Quando o botão for ativado faça essa mudança(detalhe de mudança de cor no click) ESPECIFICO PARA OPERAÇÃO*/
}
</style>