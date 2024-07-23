<template>
  <div class="game" @click="handleClick">
    <div class="game__triangle">
      <img src="../../assets/bg-triangle.svg" alt="triangle" />
    </div>
    <div class="game__body paper" data-type="paper">
      <button class="game__body-item">
        <img src="../../assets/icon-paper.svg" alt="paper" />
      </button>
    </div>

    <div class="game__body scissors" data-type="scissors">
      <button class="game__body-item">
        <img src="../../assets/icon-scissors.svg" alt="scissors" />
      </button>
    </div>
    <div class="game__body" data-type="rock">
      <button class="game__body-item">
        <img src="../../assets/icon-rock.svg" alt="rock" />
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: "Game",
  methods: {
    handleClick(event) {
      const type = event.currentTarget.getAttribute("data-type");
      console.log(type);
    },
  },
};
</script>

<style lang="scss">
.game {
  margin: 0 auto;
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
  width: 500px;
  margin-top: 64px;
  gap: 80px;

  &__triangle {
    position: absolute;
    z-index: -1;
    top: 20em;
  }
  &__body:hover {
    transform: scale(1.15);
  }
  &__body {
    width: 198px;
    height: 194px;
    background: rgb(219, 46, 77);
    border-radius: 100%;
    display: flex;
    justify-content: center;
    align-items: center;

    &.paper {
      background: rgb(70, 100, 244);
    }

    &.scissors {
      background: rgb(235, 159, 14);
    }
    &-item {
      display: flex;
      justify-content: center;
      align-items: center;
      background: linear-gradient(
        0deg,
        rgb(243, 243, 243) 0%,
        rgb(218, 218, 218) 98.342%
      );
      width: 152px;
      height: 144px;
      border-radius: 100%;
      cursor: pointer;
      border: none;
    }
  }
}
</style>
