<script setup>
import { ref } from 'vue'

const API_URL = import.meta.env.VITE_BASE_URL
const NAME_PATH = import.meta.env.VITE_NAME_PATH
const cards = ref({type: ''})
const cardInput = ref('')

async function fetchCardData(path, cardName) {
  try {
    const response = await fetch(`${API_URL}${path}${cardName}`)
    const data = await response.json()

    return data["data"] 
  } catch (error) {
    console.error(error)
  }
}

async function getCardByName() {
    cards.value = await fetchCardData(NAME_PATH, cardInput.value)
}
</script>

<template>
  <div>
    <input id="card-input" type="text" v-model="cardInput">
    <button @click="getCardByName">Get Card</button>
  </div>
  <!-- <div id="card-container">
    <div v-for="card in cards" :key="card.id" class="card-block">
      <h1>{{ card.name }}</h1>
      <p>{{ card.desc }}</p>
      <span v-if="card.type !== undefined && card.type.includes('Monster')">ATK: {{ card.atk }} / DEF: {{ card.def }}</span>
      <span>{{ card.race }} {{ card.type }}</span>
    </div>
  </div> -->
  <div id="card-container">
  <div v-for="card in cards" :key="card.id" class="card-block">
    <h1 class="card-title">{{ card.name }}</h1>
    <p class="card-description">{{ card.desc }}</p>
    <div class="card-info">
      <span v-if="card.type !== undefined && card.type.includes('Monster')" class="card-stat">ATK: {{ card.atk }} / DEF: {{ card.def }}</span>
      <span class="card-type">{{ card.race }} {{ card.type }}</span>
    </div>
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

/* Container dos cards */
#card-container {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(25%, 1fr));
  gap: 20px; /* Espaço entre as colunas */
}

/* Media query para telas menores */
@media (max-width: 768px) {
  #card-container {
    grid-template-columns: repeat(auto-fill, minmax(50%, 1fr));
  }
}

/* Media query para telas muito pequenas */
@media (max-width: 480px) {
  #card-container {
    grid-template-columns: repeat(auto-fill, minmax(100%, 1fr));
  }
}

/* Estilo dos cards */
.card-block {
  border: 1px solid #ddd; /* Uma borda mais suave */
  margin: 10px;   
  padding: 10px;
  border-radius: 8px; /* Cantos arredondados */
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1); /* Sombra suave */
  background-color: #fff; /* Fundo branco */
  transition: transform 0.2s ease-in-out; /* Efeito de transição suave */
  overflow: hidden; /* Evita que o conteúdo transborde */
  position: relative;

  /* Estilo ao passar o mouse sobre os cards */
  &:hover {
    transform: scale(1.05); /* Aumenta um pouco o tamanho ao passar o mouse */
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2); /* Sombra mais visível */
  }
}

/* Estilização dos cards */
/* .card-block {
  border: 1px solid #ddd;
  margin: 10px;
  padding: 15px;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  background-color: #fff;
  transition: transform 0.2s ease-in-out;
  overflow: hidden;
  position: relative;
  min-height: 200px; /* Altura mínima para evitar sobreposição */


/* Estilização do título do card */
.card-title {
  font-size: 1.5rem;
  margin: 0;
  color: #333;
}

/* Estilização da descrição do card */
.card-description {
  font-size: 1rem;
  color: #777;
}

/* Estilização das informações do card */
.card-info {
  position: absolute;
  bottom: 10px;
  left: 15px; /* Ajuste para não sobrepor o texto superior */
}

/* Estilização das estatísticas do card */
.card-stat {
  font-size: 1.1rem;
  font-weight: bold;
  color: #555;
}

/* Estilização do tipo do card */
.card-type {
  font-size: 1.1rem;
  color: #555;
  position: absolute;
  bottom: 10px;
  right: 15px; /* Ajuste para não sobrepor o texto superior */
}



</style>