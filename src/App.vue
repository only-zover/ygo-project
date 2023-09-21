<script setup>
import { ref } from 'vue'

const API_URL = import.meta.env.VITE_BASE_URL
const NAME_PATH = import.meta.env.VITE_NAME_PATH
const card = ref({type: ''})
let cardInput = ''

async function getCard() {
  try {
    const response = await fetch(`${API_URL}${NAME_PATH}${cardInput}`)
    const data = await response.json() 
    card.value = data["data"][0]
  } catch (error) {
    console.error(error)
  }
}

function updateCardInput(event) {
  const inputValue = event.target.value

  if (inputValue.trim() !== '') {cardInput = inputValue}
  else {cardInput = 'Mekk-Knight Avram'}
}
</script>

<template>
  <div>
    <input id="card-input" type="text" @input="updateCardInput" :value="cardInput">
    <button @click="getCard">Get Card</button>
  </div>
  <div>
    <h1>{{ card.name }}</h1>
    <h2>{{ card.desc }}</h2>
    <p v-if="card.type.includes('Monster')">ATK: {{ card.atk }} / DEF: {{ card.def }}</p>
    <p>{{ card.race }} {{ card.type }}</p>
  </div>
  <div>
    <a href="./page2.vue">To page 2</a>
  </div>
</template>
