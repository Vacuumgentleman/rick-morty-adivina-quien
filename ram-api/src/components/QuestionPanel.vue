<template>
  <div class="panel">
    <button @click="prev">⬅️</button>
    <span>{{ questions[index].text }}</span>
    <button @click="next">➡️</button>

    <button class="ask" @click="ask">Preguntar</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      index: 0,
      questions: [
        { text: "¿Está vivo?", field: "status", value: "Alive" },
        { text: "¿Está muerto?", field: "status", value: "Dead" },
        { text: "¿Es hombre?", field: "gender", value: "Male" },
        { text: "¿Es mujer?", field: "gender", value: "Female" },
        { text: "¿Es humano?", field: "species", value: "Human" },
        { text: "¿Es alien?", field: "species", value: "Alien" }
      ]
    }
  },
  methods: {
    next() {
      this.index = (this.index + 1) % this.questions.length
    },
    prev() {
      this.index =
        (this.index - 1 + this.questions.length) % this.questions.length
    },
    ask() {
      this.$emit("ask", this.questions[this.index])
    }
  }
}
</script>

<style scoped>
.panel {
  display: flex;
  gap: 10px;
  align-items: center;
  justify-content: center;
  margin-bottom: 20px;
}

.ask {
  margin-left: 10px;
}
</style>