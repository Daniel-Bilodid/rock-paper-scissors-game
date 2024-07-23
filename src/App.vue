<script>
import Score from "./components/score/Score.vue";
import Game from "./components/game/Game.vue";
import Rules from "./components/rules/Rules.vue";
export default {
  name: "App",
  components: {
    Score,
    Game,
    Rules,
  },
};
</script>

<template>
  <Score></Score>
  <Game></Game>
  <Rules></Rules>
</template>

<style></style>
