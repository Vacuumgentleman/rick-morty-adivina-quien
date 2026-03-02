<template>
  <div class="panel">
    <button v-for="q in questions" :key="q.text" @click="$emit('ask', q)">
      {{ q.text }}
    </button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      questions: [
        { text: "¿Está vivo?", field: "status", value: "Alive" },
        { text: "¿Está muerto?", field: "status", value: "Dead" },
        { text: "¿Es hombre?", field: "gender", value: "Male" },
        { text: "¿Es mujer?", field: "gender", value: "Female" },
        { text: "¿Es humano?", field: "species", value: "Human" },
        { text: "¿Es alien?", field: "species", value: "Alien" }
      ]
    }
  }
}
</script>

<style scoped>
.panel {
  display: flex;
  flex-wrap: wrap;
  gap: 6px;
  justify-content: center;
  margin-bottom: 10px;
}

button {
  background: #45a29e;
  color: #000;
  border: none;
  padding: 6px 10px;
  border-radius: 8px;
  font-size: 0.75rem;
}

button:hover {
  background: #66fcf1;
}
</style>