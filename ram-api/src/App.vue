<template>
  <HomeView v-if="screen === 'home'" @play="startGame" />
  <GameView v-else />
</template>

<script>
import HomeView from "./views/HomeView.vue"
import GameView from "./views/GameView.vue"

export default {
  components: { HomeView, GameView },
  data() {
    return {
      screen: "home"
    }
  },
  methods: {
    startGame() {
      this.screen = "game"
    }
  }
}
</script>