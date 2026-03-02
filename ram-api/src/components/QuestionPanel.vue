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
        { text: "Alive?", field: "status", value: "Alive" },
        { text: "Dead?", field: "status", value: "Dead" },
        { text: "Male?", field: "gender", value: "Male" },
        { text: "Female?", field: "gender", value: "Female" },
        { text: "Human?", field: "species", value: "Human" },
        { text: "Alien?", field: "species", value: "Alien" }
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
  padding: 6px 12px;
  font-size: 0.7rem;
  border-radius: 10px;
  background: rgba(57,255,20,0.15);
  color: var(--neon);
  border: 1px solid rgba(57,255,20,0.35);
  transition: background 0.2s, transform 0.15s;
}

button:hover {
  background: rgba(57,255,20,0.35);
  transform: scale(1.05);
}
</style>