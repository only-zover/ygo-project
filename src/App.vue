<script setup>
import { ref } from 'vue'

const API_URL = import.meta.env.VITE_BASE_URL
const NAME_PATH = import.meta.env.VITE_NAME_PATH
const cards = ref({type: ''})
const isMonsterCard = () => cards.value.type.includes('Monster');
let cardInput = ''

async function fetchCardData(pathName) {
  try {
    const response = await fetch(`${API_URL}${pathName}${cardInput}`)
    const data = await response.json()
    console.log(data["data"])
    return data["data"] 
  } catch (error) {
    console.error(error)
  }
}

async function getCardByName() {
    cards.value = await fetchCardData(NAME_PATH)
}

</script>

<template>
  <div>
    <input id="card-input" type="text" v-model="cardInput">
    <button @click="getCardByName">Get Card</button>
  </div>
  <div id="card-container">
    <div v-for="card in cards" :key="card.id" class="card-block">
      <h1>{{ card.name }}</h1>
      <p>{{ card.desc }}</p>
      <span v-if="card.type !== undefined && card.type.includes('Monster')">ATK: {{ card.atk }} / DEF: {{ card.def }}</span>
      <span>{{ card.race }} {{ card.type }}</span>
    </div>
  </div>
  <div>
    <a href="./page2.vue">To page 2</a>
  </div>
</template>

<style>
/* #card-container {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
} */

#card-container {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(25%, 1fr));
  gap: 20px; /* Espaço entre as colunas */
}

/* Media query para ajustar o layout em telas menores */
@media (max-width: 768px) {
  #card-container {
    grid-template-columns: repeat(auto-fill, minmax(50%, 1fr));
  }
}

/* Media query para ajustar o layout em telas muito pequenas */
@media (max-width: 480px) {
  #card-container {
    grid-template-columns: repeat(auto-fill, minmax(100%, 1fr));
  }
}

.card-block {
  border: 1px solid black;
  margin: 10px;
  padding: 10px;
}
</style>