<template>
    <div class="score" v-if="player">
        {{ score }}
    </div>
</template>

<script>
export default {
  name: 'score',
  props: {
    score: Number,
    player: Boolean
  }
}
</script>

<style scope>
.score {
    display: block;
    width: 100px;
    font-size: 19pt;
    font-weight: 600;
    color: greenyellow;
    background: #666;
    padding: 10px;
    text-align: center;
    margin: 0 auto;
}
</style>
