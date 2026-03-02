<template>
  <div class="home">
    <div class="card">
      <h1>Adivina Quién</h1>
      <h2>Rick & Morty Edition</h2>

      <button @click="$emit('play')">🎮 Jugar</button>

      <section class="how">
        <h3>¿Cómo jugar?</h3>
        <ul>
          <li>🤖 La máquina elige un personaje secreto</li>
          <li>❓ En cada turno puedes hacer una pregunta</li>
          <li>🧠 O puedes intentar adivinar el personaje</li>
          <li>❌ Los personajes incorrectos se descartan</li>
          <li>🏆 Ganas cuando aciertas con el personaje</li>
        </ul>
      </section>
    </div>
  </div>
</template>

<style scoped>
.home {
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  background: radial-gradient(circle, #0f2027, #203a43);
}

.card {
  background: #1b2631;
  color: white;
  padding: 2rem;
  border-radius: 16px;
  max-width: 420px;
  width: 90%;
  text-align: center;
  box-shadow: 0 0 25px rgba(0, 255, 234, 0.2);
}

h1 {
  color: #00ffea;
  margin-bottom: 0;
}

h2 {
  font-weight: normal;
  margin-top: 0.2rem;
  margin-bottom: 1.5rem;
}

button {
  background: #00ffea;
  border: none;
  padding: 12px 24px;
  font-size: 1.2rem;
  border-radius: 10px;
  cursor: pointer;
  margin-bottom: 1.5rem;
}

button:hover {
  background: #00e0d0;
}

.how {
  text-align: left;
  font-size: 0.9rem;
}

.how h3 {
  text-align: center;
  color: #00ffea;
}

ul {
  padding-left: 1rem;
}
</style>