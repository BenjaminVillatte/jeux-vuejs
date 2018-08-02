<template>
  <div id="app">
    <game />
    <player />
    <score />
  </div>
</template>

<script>
import Game from './components/Game.vue'
import Score from './components/Score.vue'
import Player from './components/Player.vue'

export default {
  name: 'app',
  components: {
    Game,
    Score,
    Player
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
</style>
