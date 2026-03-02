<template>
  <div class="container">
    <header>
      <h1>Adivina Quién</h1>
      <p>Turno {{ turns }} | Preguntas hechas: {{ questionsCount }}</p>
    </header>

    <QuestionPanel
      v-if="canAsk"
      @ask="handleQuestion"
    />

    <p v-else class="info">✔ Acción usada. Pasa al siguiente turno.</p>

    <div class="grid">
      <CharacterCard
        v-for="char in characters"
        :key="char.id"
        :character="char"
        :discarded="discardedIds.includes(char.id)"
        :selectable="canGuess"
        @select="guess(char)"
      />
    </div>

    <div v-if="gameOver" class="win">
      🎉 ¡El personaje era {{ secret.name }}!
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
      turns: 1,
      questionsCount: 0,
      actionUsed: false,
      gameOver: false
    }
  },
  computed: {
    canAsk() {
      return !this.actionUsed && !this.gameOver
    },
    canGuess() {
      return !this.actionUsed && !this.gameOver
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
      this.questionsCount++
      this.actionUsed = true

      const answer = this.secret[q.field] === q.value

      this.characters.forEach(char => {
        const match = char[q.field] === q.value
        if ((answer && !match) || (!answer && match)) {
          if (!this.discardedIds.includes(char.id)) {
            this.discardedIds.push(char.id)
          }
        }
      })

      this.nextTurn()
    },
    guess(char) {
      this.actionUsed = true

      if (char.id === this.secret.id) {
        this.gameOver = true
      } else {
        this.discardedIds.push(char.id)
        this.nextTurn()
      }
    },
    nextTurn() {
      setTimeout(() => {
        this.turns++
        this.actionUsed = false
      }, 600)
    }
  }
}
</script>

<style scoped>
.container {
  padding: 1rem;
}

header {
  text-align: center;
  margin-bottom: 1rem;
}

.info {
  text-align: center;
  color: #ccc;
}

.grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(110px, 1fr));
  gap: 10px;
}

.win {
  text-align: center;
  font-size: 1.4rem;
  margin-top: 20px;
}
</style>