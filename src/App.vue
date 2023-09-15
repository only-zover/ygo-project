<script setup>
import { ref } from 'vue'

const card = ref([])

async function getCard() {
  const response = await fetch(`https://db.ygoprodeck.com/api/v7/cardinfo.php?name=Dark Magician`)
  const data = await response.json()
  card.value = data.data[0]
  console.log(data.data[0])
}

</script>

<template>
  <div>
    <button @click="getCard">Get Card</button>
  </div>
  <div>
    <h1>{{ card.name }}</h1>
    <h2>{{ card.desc }}</h2>
    <span>ATK: {{ card.atk }} / DEF: {{ card.def }}</span>
  </div>
</template>
