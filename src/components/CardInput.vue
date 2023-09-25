  
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
</script>

<template>
  <div class="card-input-container">
    <input class="card-input" type="text" v-model="cardInput">
    <button class="get-card-btn" @click="getCardByName">Get Card</button>
  </div>
</template>  