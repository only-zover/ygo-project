<template>
    <div>
      <input type="text" v-model="inputValue">
      <button @click="handleButtonClick">Get Card</button>
    </div>
  </template>
  
  <script>
  import { ref } from 'vue'
  
  export default {
    props: {
      initialValue: String, // Valor inicial do campo de entrada
    },
    emits: ['getCardClick'], // Evento emitido quando o botão é clicado
  
    setup(props, { emit }) {
      const inputValue = ref(props.initialValue || '') // Valor inicial do campo de entrada
  
      function handleButtonClick() {
        emit('getCardClick', inputValue.value)
      }
  
      return {
        inputValue,
        handleButtonClick,
      }
    },
  }
  </script>
  