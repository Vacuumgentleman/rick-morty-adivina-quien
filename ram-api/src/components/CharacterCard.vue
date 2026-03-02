<template>
  <div
    class="card"
    :class="{ discarded }"
    @click="selectable && $emit('select')"
  >
    <img :src="character.image" :alt="character.name" />
    <div class="name">{{ character.name }}</div>
    <div v-if="discarded" class="overlay">✖</div>
  </div>
</template>

<script>
export default {
  props: {
    character: Object,
    discarded: Boolean,
    selectable: Boolean
  }
}
</script>

<style scoped>
.card {
  position: relative;
  aspect-ratio: 1 / 1; /* 🔥 CUADRADO */
  background: linear-gradient(180deg, #0b1c24, #050b10);
  border: 1px solid rgba(57,255,20,0.3);
  border-radius: 14px;
  padding: 6px;

  display: flex;
  flex-direction: column;
  justify-content: space-between;

  transition: transform 0.2s, box-shadow 0.2s;
}

.card:hover {
  transform: translateY(-3px);
  box-shadow: 0 0 20px rgba(57,255,20,0.4);
}

img {
  width: 100%;
  height: 75%;
  object-fit: cover;
  border-radius: 10px;
}

.name {
  font-size: 0.65rem;
  text-align: center;
  margin-top: 6px;
  color: var(--text-main);
}

/* DESCARTADO */
.discarded {
  opacity: 0.22;
  filter: grayscale(1);
  pointer-events: none;
}

.overlay {
  position: absolute;
  inset: 0;
  background: rgba(0,0,0,0.78);
  display: grid;
  place-items: center;
  font-size: 2.4rem;
  color: var(--danger);
  border-radius: 14px;
}
</style>