<template>
  <div class="container">
    <h2>Turno: {{ turns }}</h2>

    <QuestionPanel @ask="handleQuestion" />

    <div class="grid">
      <CharacterCard
        v-for="char in remaining"
        :key="char.id"
        :character="char"
      />
    </div>

    <div v-if="remaining.length === 1" class="win">
      🎉 ¡Tu personaje es {{ remaining[0].name }}!
      <p>Turnos usados: {{ turns }}</p>
    </div>
  </div>
</template>

<script>
import CharacterCard from "../components/CharacterCard.vue"
import QuestionPanel from "../components/QuestionPanel.vue"

export default {
  props: {
    playerCharacter: Object
  },
  components: { CharacterCard, QuestionPanel },
  data() {
    return {
      secret: null,
      remaining: [],
      turns: 0
    }
  },
  async mounted() {
    const res = await fetch("https://rickandmortyapi.com/api/character")
    const data = await res.json()
    this.remaining = data.results
    this.secret = this.remaining[Math.floor(Math.random() * this.remaining.length)]
  },
  methods: {
    handleQuestion({ field, value }) {
      this.turns++

      const answer = this.secret[field] === value

      this.remaining = this.remaining.filter(c =>
        answer ? c[field] === value : c[field] !== value
      )
    }
  }
}
</script>