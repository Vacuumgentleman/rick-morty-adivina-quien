<template>
  <div class="container">
    <h2>Turnos: {{ turns }}</h2>

    <QuestionPanel @ask="handleQuestion" />

    <div class="grid">
      <CharacterCard
        v-for="char in characters"
        :key="char.id"
        :character="char"
        :discarded="discardedIds.includes(char.id)"
      />
    </div>

    <div v-if="remaining.length === 1" class="win">
      🎉 ¡El personaje era {{ remaining[0].name }}!
      <p>Turnos usados: {{ turns }}</p>
    </div>
  </div>
</template>

<script>
import CharacterCard from "../components/CharacterCard.vue"
import QuestionPanel from "../components/QuestionPanel.vue"

export default {
  components: { CharacterCard, QuestionPanel },
  data() {
    return {
      characters: [],
      secret: null,
      discardedIds: [],
      turns: 0
    }
  },
  computed: {
    remaining() {
      return this.characters.filter(
        c => !this.discardedIds.includes(c.id)
      )
    }
  },
  async mounted() {
    const res = await fetch("https://rickandmortyapi.com/api/character")
    const data = await res.json()
    this.characters = data.results
    this.secret =
      this.characters[Math.floor(Math.random() * this.characters.length)]
  },
  methods: {
    handleQuestion(q) {
      this.turns++

      const answer = this.secret[q.field] === q.value

      this.characters.forEach(char => {
        const match = char[q.field] === q.value
        if ((answer && !match) || (!answer && match)) {
          if (!this.discardedIds.includes(char.id)) {
            this.discardedIds.push(char.id)
          }
        }
      })
    }
  }
}
</script>

<style scoped>
.grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(120px, 1fr));
  gap: 10px;
}

.win {
  text-align: center;
  margin-top: 20px;
  font-size: 1.3rem;
}
</style>