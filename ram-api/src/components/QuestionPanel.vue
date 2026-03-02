<template>
  <div class="panel">
    <select v-model="field">
      <option value="status">Estado</option>
      <option value="gender">Género</option>
      <option value="species">Especie</option>
    </select>

    <input v-model="value" placeholder="Ej: Alive" />

    <button @click="ask">Preguntar</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      field: "status",
      value: ""
    }
  },
  methods: {
    ask() {
      this.$emit("ask", { field: this.field, value: this.value })
      this.value = ""
    }
  }
}
</script>