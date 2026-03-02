<template>
  <div class="card">
    <img :src="character.image" :alt="character.name" />
    <h3>{{ character.name }}</h3>
    <p><strong>Status:</strong> {{ character.status }}</p>
    <p><strong>Species:</strong> {{ character.species }}</p>
  </div>
</template>

<script>
export default {
  name: "CharacterCard",
  props: {
    character: Object
  }
}
</script>

<style scoped>
.card {
  background: #1f2933;
  border-radius: 12px;
  padding: 1rem;
  text-align: center;
  color: #fff;
  transition: transform 0.3s;
}

.card:hover {
  transform: scale(1.05);
}

.card img {
  width: 100%;
  border-radius: 10px;
}
</style>