<template>
  <SetupView v-if="stage === 'setup'" @start="startGame" />
  <GameView v-else :playerCharacter="playerCharacter" />
</template>

<script>
import SetupView from "./views/SetupView.vue"
import GameView from "./views/GameView.vue"

export default {
  components: { SetupView, GameView },
  data() {
    return {
      stage: "setup",
      playerCharacter: null
    }
  },
  methods: {
    startGame(character) {
      this.playerCharacter = character
      this.stage = "game"
    }
  }
}
</script>