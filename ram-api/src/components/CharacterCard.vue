<template>
  <div class="card">
    <img :src="character.image" />
    <h3>{{ character.name }}</h3>
    <p>{{ character.status }} - {{ character.species }}</p>
  </div>
</template>

<script>
export default {
  props: {
    character: Object
  }
}
</script>

<style scoped>
.card {
  background: #1f2933;
  color: white;
  padding: 10px;
  border-radius: 10px;
  cursor: pointer;
}
</style>