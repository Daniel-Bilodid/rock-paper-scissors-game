<script>
import Score from "./components/score/Score.vue";
import Game from "./components/game/Game.vue";
import Rules from "./components/rules/Rules.vue";
export default {
  name: "App",

  data() {
    return {
      winCounter: 0,
    };
  },
  methods: {
    updateWinCounter(newCount) {
      this.winCounter = newCount;
    },
  },
  components: {
    Score,
    Game,
    Rules,
  },
};
</script>

<template>
  <Score :winCounter="winCounter"></Score>
  <Game :winCounter="winCounter" @updateWinCounter="updateWinCounter"></Game>
  <Rules></Rules>
</template>

<style></style>
