<template>
  <div id="app">
    <game :player="player" @score="updateScore" />
    <player @player="updatePlayer" />
    <score :player="player" :score="score" />
  </div>
</template>

<script>
import Game from './components/Game.vue'
import Score from './components/Score.vue'
import Player from './components/Player.vue'

export default {
    name: 'app',
    data () {
        return {
            score: 0,
            player: false
        }
    },
    components: {
        Game,
        Score,
        Player
    },
    methods: {
        updateScore (score) {
            this.score = score
        },
        updatePlayer () {
            this.player = true
        }
    }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  height: 500px;
  display: block;
}
</style>
