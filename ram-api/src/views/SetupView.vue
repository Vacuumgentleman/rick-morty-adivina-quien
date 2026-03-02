<template>
  <div class="container">
    <h1>Elige tu personaje</h1>

    <div class="grid">
      <CharacterCard
        v-for="char in characters"
        :key="char.id"
        :character="char"
        @click="selectCharacter(char)"
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
    const res = await fetch("https://rickandmortyapi.com/api/character")
    const data = await res.json()
    this.characters = data.results
  },
  methods: {
    selectCharacter(character) {
      this.$emit("start", character)
    }
  }
}
</script>