<template>
  <div class="game">

    <!-- NAVBAR -->
    <header class="navbar">
      <router-link to="/" class="nav-back">⟵ Exit</router-link>

      <div class="nav-title">
        <h1>Portal Guess</h1>
        <span>Rick & Morty</span>
      </div>

      <div class="nav-stats">
        <div>
          <strong>{{ turns }}</strong>
          <small>Turns</small>
        </div>
        <div>
          <strong>{{ questionsCount }}</strong>
          <small>Questions</small>
        </div>
      </div>
    </header>

    <!-- CONTENT -->
    <main class="content">
      <div class="layout">

        <!-- BOARD -->
        <section class="board">
          <CharacterCard
            v-for="c in characters"
            :key="c.id"
            :character="c"
            :discarded="discardedIds.includes(c.id)"
            :selectable="!actionUsed && !gameOver"
            @select="guess(c)"
          />
        </section>

        <!-- SIDEBAR -->
        <aside class="sidebar">
          <QuestionPanel
            :disabled="actionUsed || gameOver"
            @ask="handleQuestion"
          />
        </aside>

      </div>
    </main>

    <!-- WIN MODAL -->
    <div v-if="gameOver" class="overlay">
      <div class="modal">
        <h2>🌀 You guessed it!</h2>

        <div class="results">
          <div>
            <strong>{{ questionsCount }}</strong>
            <span>Questions</span>
          </div>
          <div>
            <strong>{{ turns }}</strong>
            <span>Turns</span>
          </div>
          <div class="score">
            <strong>{{ score }}</strong>
            <span>Score</span>
          </div>
        </div>

        <button class="portal-btn" @click="restart">
          🧪 Jump into another portal
        </button>
      </div>
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
    score() {
      const raw = 1000 - (this.questionsCount * 40 + this.turns * 20)
      return Math.max(0, raw)
    }
  },
  async mounted() {
    await this.loadGame()
  },
  methods: {
    async loadGame() {
      const page = Math.floor(Math.random() * 42) + 1
      const res = await fetch(
        `https://rickandmortyapi.com/api/character?page=${page}`
      )
      const data = await res.json()

      this.characters = data.results
        .filter(c => c.image)
        .slice(0, 20)

      this.secret =
        this.characters[Math.floor(Math.random() * this.characters.length)]
    },

    handleQuestion(q) {
      this.questionsCount++
      this.actionUsed = true

      const answer =
        q.field === "episode.length"
          ? this.secret.episode.length > 1
          : q.field.includes(".")
            ? q.field.split(".").reduce((o, k) => o?.[k], this.secret) === q.value
            : this.secret[q.field] === q.value

      this.characters.forEach(c => {
        const match =
          q.field === "episode.length"
            ? c.episode.length > 1
            : q.field.includes(".")
              ? q.field.split(".").reduce((o, k) => o?.[k], c) === q.value
              : c[q.field] === q.value

        if ((answer && !match) || (!answer && match)) {
          if (!this.discardedIds.includes(c.id)) {
            this.discardedIds.push(c.id)
          }
        }
      })

      setTimeout(() => {
        this.turns++
        this.actionUsed = false
      }, 400)
    },

    guess(c) {
      this.actionUsed = true

      if (c.id === this.secret.id) {
        this.gameOver = true
      } else {
        this.discardedIds.push(c.id)
      }

      setTimeout(() => {
        this.turns++
        this.actionUsed = false
      }, 400)
    },

    async restart() {
      this.characters = []
      this.secret = null
      this.discardedIds = []
      this.turns = 1
      this.questionsCount = 0
      this.actionUsed = false
      this.gameOver = false

      await this.loadGame()
    }
  }
}
</script>

<style scoped>
/* ===== NAVBAR ===== */
.navbar {
  position: sticky;
  top: 0;
  z-index: 100;
  height: 72px;
  padding: 0 18px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  background: linear-gradient(90deg, #02131c, #031f2d);
  border-bottom: 1px solid rgba(0,255,170,.35);
}

.nav-back {
  color: #00ffb3;
  text-decoration: none;
  font-weight: 600;
}

.nav-title h1 {
  color: #00ffb3;
  font-size: 1.1rem;
  margin: 0;
}

.nav-title span {
  font-size: .7rem;
  color: #8affdc;
}

.nav-stats {
  display: flex;
  gap: 14px;
}

.nav-stats div {
  text-align: center;
}

.nav-stats strong {
  color: #00ffb3;
}

/* ===== LAYOUT ===== */
.layout {
  display: grid;
  grid-template-columns: 1fr 320px;
  gap: 16px;
}

.board {
  display: grid;
  grid-template-columns: repeat(5, 1fr);
  gap: 14px;
}

.sidebar {
  position: sticky;
  top: 88px;
  background: #050e13;
  border-radius: 14px;
  padding: 12px;
}

/* ===== MODAL ===== */
.overlay {
  position: fixed;
  inset: 0;
  background: rgba(0,0,0,.75);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 200;
}

.modal {
  background: #071a24;
  border-radius: 16px;
  padding: 26px;
  width: 320px;
  text-align: center;
  animation: pop .25s ease;
}

.modal h2 {
  color: #00ffb3;
  margin-bottom: 18px;
}

.results {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 10px;
  margin-bottom: 20px;
}

.results div {
  background: #020c12;
  border-radius: 10px;
  padding: 10px;
}

.results span {
  font-size: .7rem;
  color: #7eeed1;
}

.score strong {
  color: #00ffb3;
  font-size: 1.4rem;
}

/* ===== PORTAL BUTTON ===== */
.portal-btn {
  position: relative;
  width: 100%;
  padding: 14px 18px;
  border-radius: 14px;
  border: none;
  font-weight: 800;
  font-size: .95rem;
  letter-spacing: .4px;
  color: #012019;
  background: radial-gradient(
    circle at top left,
    #7dffe1,
    #00ffb3 60%
  );
  cursor: pointer;
  overflow: hidden;
  box-shadow:
    0 0 12px rgba(0,255,179,.6),
    0 0 32px rgba(0,255,179,.35);
  transition: transform .15s ease, box-shadow .15s ease;
}

.portal-btn::before {
  content: "";
  position: absolute;
  inset: -2px;
  border-radius: inherit;
  background: linear-gradient(
    120deg,
    transparent 30%,
    rgba(255,255,255,.7),
    transparent 70%
  );
  opacity: .35;
  animation: portalSpin 2.5s linear infinite;
}

.portal-btn:hover {
  transform: translateY(-2px) scale(1.02);
  box-shadow:
    0 0 18px rgba(0,255,179,.9),
    0 0 40px rgba(0,255,179,.6);
}

.portal-btn:active {
  transform: scale(.97);
}

@keyframes portalSpin {
  from { transform: rotate(0deg); }
  to { transform: rotate(360deg); }
}

@keyframes pop {
  from { transform: scale(.85); opacity: 0 }
  to { transform: scale(1); opacity: 1 }
}

/* ===== MOBILE ===== */
@media (max-width: 900px) {
  .layout {
    grid-template-columns: 1fr;
  }

  .sidebar {
    position: fixed;
    bottom: 0;
    left: 0;
    right: 0;
    z-index: 90;
    border-radius: 14px 14px 0 0;
  }

  .board {
    margin-bottom: 260px;
    grid-template-columns: repeat(2, 1fr);
  }
}
</style>