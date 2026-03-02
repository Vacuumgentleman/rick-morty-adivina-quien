<template>
  <div class="container">
    <h1>Adivina el Personaje 🕵️‍♂️</h1>

    <!-- BOTONES DE PREGUNTAS -->
    <div class="filters">
      <button @click="filterByStatus('Alive')">¿Está vivo?</button>
      <button @click="filterBySpecies('Human')">¿Es humano?</button>
      <button @click="filterByGender('Male')">¿Es hombre?</button>
      <button class="reset" @click="resetGame">Reiniciar</button>
    </div>

    <p v-if="loading">Cargando personajes...</p>

    <div class="grid" v-if="!loading">
      <CharacterCard
        v-for="character in characters"
        :key="character.id"
        :character="character"
        @guess="makeGuess"
      />
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import CharacterCard from '../components/CharacterCard.vue'

const characters = ref([])
const secretCharacter = ref(null)
const loading = ref(true)

onMounted(async () => {
  const res = await fetch('https://rickandmortyapi.com/api/character')
  const data = await res.json()
  characters.value = data.results

  const random = Math.floor(Math.random() * characters.value.length)
  secretCharacter.value = characters.value[random]

  loading.value = false
})

function filterByStatus(value) {
  const answer = secretCharacter.value.status === value
  characters.value = characters.value.filter(
    c => (c.status === value) === answer
  )
}

function filterBySpecies(value) {
  const answer = secretCharacter.value.species === value
  characters.value = characters.value.filter(
    c => (c.species === value) === answer
  )
}

function filterByGender(value) {
  const answer = secretCharacter.value.gender === value
  characters.value = characters.value.filter(
    c => (c.gender === value) === answer
  )
}

function makeGuess(character) {
  if (character.id === secretCharacter.value.id) {
    alert('🎉 ¡Ganaste!')
  } else {
    alert('❌ Intenta de nuevo')
  }
}

function resetGame() {
  window.location.reload()
}
</script>

<style scoped>
.container {
  padding: 20px;
}

h1 {
  text-align: center;
}

.filters {
  display: flex;
  gap: 10px;
  justify-content: center;
  flex-wrap: wrap;
  margin-bottom: 20px;
}

.filters button {
  padding: 8px 14px;
  border-radius: 8px;
  border: none;
  background: #4caf50;
  color: white;
  cursor: pointer;
}

.reset {
  background: #f44336;
}

.grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
  gap: 20px;
}
</style>