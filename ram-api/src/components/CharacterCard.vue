<template>
  <div
    class="card"
    :class="{ discarded }"
    @click="selectable && $emit('select')"
  >
    <img :src="character.image" />
    <h4>{{ character.name }}</h4>
    <div v-if="discarded" class="x">❌</div>
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
  background: #1f2933;
  color: white;
  border-radius: 8px;
  padding: 5px;
  cursor: pointer;
  transition: transform 0.2s;
}

.card:hover {
  transform: scale(1.03);
}

.card img {
  width: 100%;
  border-radius: 6px;
}

.discarded {
  opacity: 0.25;
  pointer-events: none;
}

.x {
  position: absolute;
  top: 4px;
  right: 6px;
  font-size: 1.3rem;
}
</style>