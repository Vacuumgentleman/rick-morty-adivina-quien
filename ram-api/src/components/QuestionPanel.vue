<template>
  <div class="questions">

    <div
      v-for="group in questionGroups"
      :key="group.title"
      class="group"
    >
      <h5>{{ group.title }}</h5>

      <div class="options">
        <button
          v-for="q in group.questions"
          :key="q.text"
          :disabled="disabled"
          @click="$emit('ask', q)"
        >
          {{ q.text }}
        </button>
      </div>
    </div>

  </div>
</template>

<script>
export default {
  props: {
    disabled: Boolean
  },
  data() {
    return {
      questionGroups: [
        {
          title: "Status",
          questions: [
            { text: "Alive?", field: "status", value: "Alive" },
            { text: "Dead?", field: "status", value: "Dead" },
            { text: "Unknown?", field: "status", value: "unknown" }
          ]
        },
        {
          title: "Gender",
          questions: [
            { text: "Male?", field: "gender", value: "Male" },
            { text: "Female?", field: "gender", value: "Female" },
            { text: "Genderless?", field: "gender", value: "Genderless" },
            { text: "Unknown?", field: "gender", value: "unknown" }
          ]
        },
        {
          title: "Species",
          questions: [
            { text: "Human?", field: "species", value: "Human" },
            { text: "Alien?", field: "species", value: "Alien" },
            { text: "Humanoid?", field: "species", value: "Humanoid" }
          ]
        },
        {
          title: "Origin",
          questions: [
            { text: "From Earth?", field: "origin.name", value: "Earth" },
            { text: "Unknown origin?", field: "origin.name", value: "unknown" }
          ]
        },
        {
          title: "Episodes",
          questions: [
            {
              text: "Appears in multiple episodes?",
              field: "episode.length",
              value: "multiple"
            }
          ]
        }
      ]
    }
  }
}
</script>

<style scoped>
.questions {
  display: flex;
  flex-direction: column;
  gap: 12px;
}

.group h5 {
  font-size: 0.65rem;
  color: var(--neon);
  margin-bottom: 6px;
  text-transform: uppercase;
  letter-spacing: 0.05em;
}

.options {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 6px;
}

button {
  font-size: 0.6rem;
  padding: 6px;
  border-radius: 8px;
  background: #0c1f27;
  border: 1px solid rgba(57,255,20,0.3);
  color: var(--text-main);
}

button:disabled {
  opacity: 0.4;
}
</style>