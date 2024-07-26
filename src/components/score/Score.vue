<template>
  <div class="score">
    <div class="score__wrapper">
      <h1 class="score__title">ROCK PAPER SCISSORS</h1>

      <div class="score__count">
        <div class="score__count-name">SCORE</div>

        <div class="score__count-number">{{ winCounter }}</div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Score",
  props: ["winCounter"],
};
</script>

<style lang="scss">
@import "../../variables";
.score {
  width: 700px;
  height: 150px;
  border: 3px solid rgba(255, 255, 255, 0.29);
  border-radius: 15px;
  margin: 0 auto;
  &__title {
    width: 159px;
    height: 96px;

    color: rgb(255, 255, 255);
    font-family: $barlow;
    font-size: 40px;
    font-weight: 700;
    line-height: 32px;
    letter-spacing: 0px;
    text-align: left;
    margin-left: 32px;
  }
  &__wrapper {
    display: flex;
    justify-content: space-between;
  }

  &__count {
    width: 150px;
    height: 114px;
    border-radius: 8px;

    box-shadow: 0px 3px 3px 0px rgba(0, 0, 0, 0.2);
    background: linear-gradient(
      0deg,
      rgb(243, 243, 243),
      rgb(255, 255, 255) 100%
    );
    margin-top: 18px;
    margin-right: 24px;

    &-name {
      color: rgb(42, 69, 194);
      font-family: $barlow;
      font-size: 16px;
      font-weight: 600;
      line-height: 19px;
      letter-spacing: 2.5px;
      margin-top: 16px;
    }
    &-number {
      color: rgb(86, 84, 104);
      font-family: $barlow;
      font-size: 64px;
      font-weight: 700;
      line-height: 64px;
      letter-spacing: 0px;
      text-align: center;
    }
  }
}
</style>
