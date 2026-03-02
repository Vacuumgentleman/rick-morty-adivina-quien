<template>
  <div class="game">
    <header>
      <router-link to="/" class="back">⬅ Inicio</router-link>
      <h2>Adivina Quién</h2>
      <p>Turno {{ turns }} · Preguntas {{ questionsCount }}</p>
    </header>

    <QuestionPanel
      v-if="!actionUsed && !gameOver"
      @ask="handleQuestion"
    />

    <p v-else-if="!gameOver" class="info">
      Acción usada, pasando al siguiente turno…
    </p>

    <div class="grid">
      <CharacterCard
        v-for="char in characters"
        :key="char.id"
        :character="char"
        :discarded="discardedIds.includes(char.id)"
        :selectable="!actionUsed && !gameOver"
        @select="guess(char)"
      />
    </div>

    <div v-if="gameOver" class="win">
      🎉 El personaje era <strong>{{ secret.name }}</strong><br />
      Turnos usados: {{ turns }}
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

      this.characters.forEach(c => {
        const match = c[q.field] === q.value
        if ((answer && !match) || (!answer && match)) {
          if (!this.discardedIds.includes(c.id)) {
            this.discardedIds.push(c.id)
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
      }, 500)
    }
  }
}
</script>

<style scoped>
.game {
  max-width: 1400px;
  margin: auto;
  padding: 1rem;
}

header {
  text-align: center;
  margin-bottom: 0.5rem;
}

.back {
  display: inline-block;
  margin-bottom: 5px;
  color: #66fcf1;
  font-size: 0.9rem;
}

.info {
  text-align: center;
  color: #aaa;
  margin: 8px 0;
}

.grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(95px, 1fr));
  gap: 10px;
}

.win {
  text-align: center;
  margin-top: 1rem;
  font-size: 1.3rem;
  color: #66fcf1;
}
</style>