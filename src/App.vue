<script setup>
import { ref } from 'vue'

const API_URL = import.meta.env.VITE_BASE_URL
const NAME_PATH = import.meta.env.VITE_NAME_PATH
const cards = ref([])
const cardInput = ref('')

async function getCardByName() {
  const response = await fetch(`${API_URL}${NAME_PATH}${cardInput.value}`)
  const data = await response.json()

  cards.value = data["data"] 
}

function cardClass(card) {
  const cardTypes = ['Spell', 'Trap', 'Normal', 'Link', 'Fusion', 'Synchro', 'XYZ', 'Pendulum', 'Ritual', 'Token', 'Monster'];

  for (const type of cardTypes) {
    if (card.type?.includes(type)) {
      return `${type.toLowerCase()}-card`;
    }
  }

  return '';
}

</script>

<template>
  <div class="card-input-container">
    <input class="card-input" type="text" v-model="cardInput">
    <button class="get-card-btn" @click="getCardByName">Get Card</button>
  </div>
  <div id="card-container">
  <div v-for="card in cards" :key="card.id" :class="cardClass(card)" class="card-block">
    <h1 class="card-title">{{ card.name }}</h1>
    <p class="card-description">{{ card.desc }}</p>
    <span class="card-type">{{ card.race }} {{ card.type }}</span>
    <p class="card-stat" v-if="card.type?.includes('Monster')">ATK: {{ card.atk }} / DEF: {{ card.def }}</p>
  </div>
</div>
</template>

<style>
.spell-card {
  background-image: linear-gradient(to bottom, #4CAF50, #357a38);
}

.trap-card {
  background-image: linear-gradient(to bottom, #FF69B4, #FF1493);
}

.monster-card {
  background-image: linear-gradient(to bottom, #FF9800, #E65100);
}

.normal-card {
  background-image: linear-gradient(to bottom, #FFD700, #FFA500);
}

.link-card {
  background-image: linear-gradient(to bottom, #2196F3, #1976D2);
}

.fusion-card {
  background-image: linear-gradient(to bottom, #9C27B0, #673AB7);
}

.synchro-card {
  background-color: #fff;

}

.synchro-card h1, .synchro-card p, .synchro-card span {
  color: #000000;
}

.xyz-card {
  background-color: #000;
}

.pendulum-card {
  background-image: linear-gradient(to bottom, #E65100, #fff, #357a38);
}

.pendulum-card h1, .pendulum-card p, .pendulum-card span {
  color: #000000;
}

.ritual-card {
  background-image: linear-gradient(to bottom, #87CEEB, #00BFFF);
}

.token-card {
  background-color:#666666;
}

.card-input-container {
  display: flex;
  align-items: center;
  justify-content: center;
}

.card-input {
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 5px;
  margin-right: 10px;
}

.get-card-btn {
  padding: 10px;
  border: none;
  border-radius: 5px;
  background-color: #007bff;
  color: #fff;
  cursor: pointer;
}

.get-card-btn:hover {
  background-color: #0069d9;
}


#card-container {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(25%, 1fr));
  gap: 20px;
}

@media (max-width: 768px) {
  #card-container {
    grid-template-columns: repeat(auto-fill, minmax(50%, 1fr));
  }
}

@media (max-width: 480px) {
  #card-container {
    grid-template-columns: repeat(auto-fill, minmax(100%, 1fr));
  }
}

.card-block {
  border: 1px solid #ddd;
  margin: 10px;
  padding: 10px;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  transition: transform 0.2s ease-in-out;
  overflow: hidden;
  position: relative;
  min-height: 200px;

  &:hover {
    transform: scale(1.05);
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
  }
}

.card-title {
  font-size: 1.5rem;
  margin: 0;
  color: #fff;
  /* Adicione mais estilos de acordo com suas preferências */
}

.card-description {
  font-size: 1rem;
  color: #fff;
  /* Adicione mais estilos de acordo com suas preferências */
}

.card-stat {
  font-size: 1.1rem;
  font-weight: bold;
  color: #fff;
  /* Adicione mais estilos de acordo com suas preferências */
}

.card-type {
  font-size: 1.1rem;
  color: #fff;
  position: absolute;
  bottom: 10px;
  right: 15px;
  /* Adicione mais estilos de acordo com suas preferências */
}


.card-info {
  position: absolute;
  bottom: 10px;
  left: 15px; 
}
</style>