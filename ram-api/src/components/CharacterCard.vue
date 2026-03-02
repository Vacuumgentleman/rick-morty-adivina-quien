<template>
  <div class="card" :class="{ discarded }">
    <img :src="character.image" />
    <h4>{{ character.name }}</h4>
    <div v-if="discarded" class="x">❌</div>
  </div>
</template>

<script>
export default {
  props: {
    character: Object,
    discarded: Boolean
  }
}
</script>

<style scoped>
.card {
  position: relative;
  background: #1f2933;
  border-radius: 8px;
  padding: 5px;
}

.card img {
  width: 100%;
  border-radius: 6px;
}

.discarded {
  opacity: 0.3;
}

.x {
  position: absolute;
  top: 5px;
  right: 5px;
  font-size: 1.5rem;
}
</style>