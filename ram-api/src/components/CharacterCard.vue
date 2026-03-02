<template>
  <div
    class="card"
    :class="{ discarded }"
    @click="selectable && $emit('select')"
  >
    <img :src="character.image" />
    <span>{{ character.name }}</span>
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
  background: linear-gradient(180deg, #0b1c24, #050b10);
  border: 1px solid rgba(57,255,20,0.25);
  border-radius: 12px;
  padding: 4px;
  text-align: center;
  transition: transform 0.2s, box-shadow 0.2s;
}

.card:hover {
  transform: scale(1.06);
  box-shadow: 0 0 15px rgba(57,255,20,0.35);
}

img {
  width: 100%;
  height: 90px;
  object-fit: cover;
  border-radius: 8px;
}

span {
  display: block;
  font-size: 0.62rem;
  margin-top: 4px;
}

.discarded {
  opacity: 0.25;
  filter: grayscale(1);
  pointer-events: none;
}

.overlay {
  position: absolute;
  inset: 0;
  background: rgba(0,0,0,0.75);
  display: grid;
  place-items: center;
  font-size: 2rem;
  color: var(--danger);
  border-radius: 12px;
}
</style>