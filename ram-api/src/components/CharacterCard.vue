<template>
  <div
    class="card"
    :class="{ discarded }"
    @click="selectable && $emit('select')"
  >
    <img :src="character.image" />
    <h4>{{ character.name }}</h4>
    <div v-if="discarded" class="overlay">❌</div>
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
  background: #1b2631;
  border-radius: 10px;
  padding: 4px;
  text-align: center;
  transition: transform 0.2s;
}

.card:hover {
  transform: scale(1.04);
}

img {
  width: 100%;
  height: 95px;
  object-fit: cover;
  border-radius: 6px;
}

h4 {
  font-size: 0.65rem;
  margin-top: 4px;
}

.discarded {
  opacity: 0.3;
  pointer-events: none;
}

.overlay {
  position: absolute;
  inset: 0;
  background: rgba(0, 0, 0, 0.65);
  display: grid;
  place-items: center;
  font-size: 2rem;
}
</style>