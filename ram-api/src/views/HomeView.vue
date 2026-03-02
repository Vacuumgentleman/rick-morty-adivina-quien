<template>
  <div class="container">
    <h1>Rick and Morty Explorer</h1>

    <div class="grid">
      <CharacterCard
        v-for="char in characters"
        :key="char.id"
        :character="char"
      />
    </div>
  </div>
</template>

<script>
import CharacterCard from "../components/CharacterCard.vue"

export default {
  components: { CharacterCard },
  data() {
    return {
      characters: []
    }
  },
  async mounted() {
    const response = await fetch("https://rickandmortyapi.com/api/character")
    const data = await response.json()
    this.characters = data.results
  }
}
</script>

<style scoped>
.container {
  padding: 2rem;
}

h1 {
  text-align: center;
  margin-bottom: 2rem;
  color: #00ffea;
}

.grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(220px, 1fr));
  gap: 1.5rem;
}
</style>