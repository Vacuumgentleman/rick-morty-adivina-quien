<template>
  <div class="home">
    <div class="card">
      <h1>Adivina Quién</h1>
      <h2>Rick & Morty Edition</h2>

      <router-link to="/game" class="play">
        🎮 Jugar
      </router-link>

      <section>
        <h3>¿Cómo jugar?</h3>
        <ul>
          <li>🤖 La IA elige un personaje secreto</li>
          <li>❓ Haz una sola pregunta por turno</li>
          <li>🧠 O intenta adivinar el personaje</li>
          <li>❌ Los personajes descartados se marcan</li>
          <li>🏆 Adivina en el menor número de turnos</li>
        </ul>
      </section>
    </div>
  </div>
</template>

<style scoped>
.home {
  min-height: 100vh;
  display: grid;
  place-items: center;
}

.card {
  background: #141a22;
  padding: 2rem;
  border-radius: 20px;
  max-width: 420px;
  width: 90%;
  text-align: center;
  box-shadow: 0 0 40px rgba(0, 255, 234, 0.15);
}

h1 {
  color: #66fcf1;
  margin-bottom: 0.3rem;
}

h2 {
  font-weight: normal;
  font-size: 1rem;
  margin-bottom: 1.5rem;
}

.play {
  display: inline-block;
  background: #66fcf1;
  color: #000;
  padding: 14px 30px;
  border-radius: 14px;
  font-size: 1.2rem;
  margin-bottom: 1.5rem;
}

section {
  text-align: left;
  font-size: 0.9rem;
}

section h3 {
  text-align: center;
  color: #66fcf1;
  margin-bottom: 0.5rem;
}

ul {
  padding-left: 1.2rem;
}
</style>