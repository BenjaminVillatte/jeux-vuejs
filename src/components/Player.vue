<template>
    <div class="player">
        <span v-html="welcomeMessage" :class="{hide: !player}"></span>

        <form @submit.prevent="setPlayer" :class="{hide: player}">
            <input name="player" placeholder="Entrez votre nom de joueur" />
            <button  type="submit">Jouer</button>
        </form>
    </div>
</template>

<script>
export default {
  name: 'player',
  data: function () {
    return {
      player: '',
      welcomeMessage: ''
    }
  },
  updated: function () {
    this.welcomeMessage = `Bonjour <span class="player">${this.player}</span> !`
  },
  methods: {
    setPlayer: function (event) {
      let playername = event.target[0].value

      if (!playername) {
        window.alert('Merci de renseigner votre pseudo')
        return
      }
      this.player = playername
      this.$emit('player')
    }
  }
}
</script>

<style scoped>
.player {
    text-align: center;
}
.hide {
    display: none;
}
</style>
