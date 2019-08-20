<template>
    <div class="content">
        <div id="game" class="game" v-on:click="clickOnInterface" :class="{wait: !player || stopped}">
            <span class="time" v-if="!stopped">{{ time }}</span>
            <span class="round"
                v-if="player && !stopped"
                :style="roundStyle"
                :class="{bonus: bonusActivated, badColor: badColorActivated}"
                @click.stop="clickOnRound"
                @click.alt.stop="bonus"></span>
        </div>
        <div class="log">
            <p v-for="item in userLogs" :key="item.id">
                #{{ item.id }} - {{ item.message }}
            </p>
        </div>
    </div>
</template>

<script>
export default {
  name: 'game',
  props: {
    player: Boolean
  },
  data: function () {
    return {
      click: 0,
      time: 0,
      roundStyle: {
        width: '50px',
        height: '50px',
        margin: '20% 20%'
      },
      bonusActivated: false,
      badColorActivated: false,
      collection: ['message 1', 'message 2', 'message 3'],
      stopped: true,
      intervalID: null
    }
  },
  computed: {
    userLogs () {
      return this.collection.filter(item => {
        return item.type === 'user'
      })
    }
  },
  watch: {
    click: function () {
      this.updateRound()
      this.$emit('score', this.click)
    },
    player () {
      this.stopped = false
      this.time = 10
      let self = this

      this.intervalID = setInterval(function () {
        self.updateTime()
      }, 1000)
    }
  },
  methods: {
    updateTime () {
      if (this.time === 0) {
        this.stopped = true
      }

      if (!this.stopped) {
        this.time--
      }
    },
    clickOnRound: function (event) {
      setTimeout(this.updateRound, 1000)
      this.updateClick(true)
      this.addLog(`BRAVO !`)
    },
    clickOnInterface: function (event) {
      this.updateClick(false)
      this.addLog(`HO NON :( -1`)
    },
    bonus: function (event) {
      if (this.bonusActivated) {
        this.updateClick(true)
        this.addLog(`PERFECT ! +2`)
      } else {
        this.updateClick(false)
        this.addLog(`??? -1`)
      }
    },
    updateClick (increment) {
      if (!this.player || this.stopped) {
        return
      }
      if (increment) {
        this.click++
      } else {
        this.click--
      }
    },
    updateRound: function () {
      const width = document.getElementById('game').offsetWidth
      const height = document.getElementById('game').offsetHeight

      let size = Math.random() * (100 - 10) + 10
      let top = Math.random() * (height - 5) + 5
      let left = Math.random() * (width - 5) + 5

      this.badColorActivated = size < 20
      this.bonusActivated = size > 80

      this.addLog({
        size: size,
        top: top,
        left: left
      }, 'round')

      this.roundStyle.width = this.roundStyle.height = `${size}px`
      this.roundStyle.margin = `${top}px ${left}px`
    },
    addLog (message, type) {
      if (!this.player || this.stopped) {
        return
      }

      let typeofMessage = type || 'user'
      this.collection.unshift({id: this.collection.length, message: message, type: typeofMessage})
    },
    destoyed () {
      clearInterval(this.intervalID)
    }
  }
}
</script>

<style scoped>
.content {
    height: 550px;
}
.log {
    width: 100%;
    height: 35px;
    background: #666;
    color: white;
    display: block;
    overflow: hidden;
    padding: 6px;
    text-align: center;
}
.game {
    width: 100%;
    height: 90%;
    display: block;
    background: #000000;
    opacity: 1;
    transition: opacity 1s;
}
.round {
    background: aliceblue;
    border-radius: 9999px;
    position: absolute;
    transition: width 2s, height 2s, margin 0.5s;
}
.bonus {
    background: indianRed;
}
.badColor {
    background: #090f0f
}
.wait {
    opacity: 0.3;
}
.time {
    position: absolute;
    font-size: 90pt;
    padding-left: 30px;
    color: darkgoldenrod;
    opacity: 0.2;
}
</style>
