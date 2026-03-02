<template>
  <div class="game">
    <header class="hud">
      <router-link to="/" class="back">← Exit Portal</router-link>
      <h2>Portal Guess</h2>
      <p>Turn {{ turns }} · Questions {{ questionsCount }}</p>
    </header>

    <QuestionPanel
      v-if="!actionUsed && !gameOver"
      @ask="handleQuestion"
    />

    <p v-else-if="!gameOver" class="info">
      Processing reality shift…
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
      <h3>PORTAL LOCKED</h3>
      <p>The character was <strong>{{ secret.name }}</strong></p>
      <p>Turns used: {{ turns }}</p>
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
      }, 600)
    }
  }
}
</script>

<style scoped>
.game {
  max-width: 1500px;
  margin: auto;
  padding: 1rem;
}

.hud {
  text-align: center;
  margin-bottom: 0.8rem;
}

.hud h2 {
  color: var(--neon);
}

.hud p {
  font-size: 0.8rem;
  color: var(--text-muted);
}

.back {
  display: inline-block;
  font-size: 0.8rem;
  color: var(--neon-soft);
  margin-bottom: 4px;
}

.info {
  text-align: center;
  font-size: 0.8rem;
  color: var(--text-muted);
  margin-bottom: 8px;
}

.grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(92px, 1fr));
  gap: 10px;
}

.win {
  text-align: center;
  margin-top: 1.2rem;
  color: var(--neon);
}
</style>