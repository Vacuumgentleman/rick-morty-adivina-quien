<template>
  <div class="home">
    <div class="portal-card">
      <h1>PORTAL GUESS</h1>
      <h2>Rick & Morty</h2>

      <router-link to="/game" class="play-btn">
        ENTER PORTAL
      </router-link>

      <div class="rules">
        <h3>How to play</h3>
        <ul>
          <li>The AI chooses a secret character</li>
          <li>You can ask only one question per turn</li>
          <li>Or guess the character directly</li>
          <li>Discard characters to narrow it down</li>
          <li>Guess in the fewest turns possible</li>
        </ul>
      </div>
    </div>
  </div>
</template>

<style scoped>
.home {
  min-height: 100vh;
  display: grid;
  place-items: center;
}

.portal-card {
  background: linear-gradient(
    180deg,
    rgba(11, 28, 36, 0.95),
    rgba(5, 11, 16, 0.95)
  );
  border: 1px solid rgba(57,255,20,0.35);
  border-radius: 22px;
  padding: 2.5rem 2.2rem;
  width: 90%;
  max-width: 460px;
  text-align: center;
  box-shadow:
    0 0 40px rgba(57,255,20,0.25),
    inset 0 0 25px rgba(57,255,20,0.08);
}

h1 {
  color: var(--neon);
  font-size: 2.2rem;
}

h2 {
  font-size: 1rem;
  font-weight: 400;
  margin-bottom: 1.8rem;
  color: var(--text-muted);
}

.play-btn {
  display: inline-block;
  margin-bottom: 1.8rem;
  padding: 14px 34px;
  border-radius: 14px;
  font-family: "Orbitron", sans-serif;
  font-weight: 600;
  background: radial-gradient(circle, var(--neon), var(--neon-soft));
  color: #00140a;
  box-shadow: 0 0 20px rgba(57,255,20,0.7);
  transition: transform 0.2s, box-shadow 0.2s;
}

.play-btn:hover {
  transform: scale(1.05);
  box-shadow: 0 0 30px rgba(57,255,20,0.9);
}

.rules {
  text-align: left;
  font-size: 0.9rem;
}

.rules h3 {
  text-align: center;
  margin-bottom: 0.6rem;
  color: var(--neon-soft);
}

.rules ul {
  padding-left: 1.1rem;
  color: var(--text-muted);
}
</style>