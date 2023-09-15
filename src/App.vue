<script setup>
import { ref } from 'vue'

const API_URL = "https://db.ygoprodeck.com/api/v7/cardinfo.php?"
const CARD = ref([])
const status = ref("")

async function getCard() {
  const response = (await fetch(`${API_URL}name=Dark Magician`))
  const data = await response.json()
  const card = CARD.value = data.data[0]
  status.value = `\nATK: ${card.atk} / DEF: ${card.def}`
}

</script>

<template>
  <div>
    <a href="./page2.vue">To page 2</a>
  </div>
  <div>
    <button @click="getCard">Get Card</button>
  </div>
  <div>
    <h1>{{ CARD.name }}</h1>
    <h2>{{ CARD.desc }}</h2>
    <p>{{ status }}</p>
  </div>
</template>
