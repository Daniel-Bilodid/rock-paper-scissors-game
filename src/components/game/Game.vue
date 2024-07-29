<template>
  <transition name="fade">
    <div class="game">
      <transition-group name="slide">
        <div v-if="!selectedType" class="game__triangle">
          <img src="../../assets/bg-triangle.svg" alt="triangle" />
        </div>
        <div
          v-if="!selectedType || selectedType === 'paper'"
          class="game__body paper"
          data-type="paper"
        >
          <button class="game__body-item" @click="handleClick('paper')">
            <img src="../../assets/icon-paper.svg" alt="paper" />
          </button>
        </div>

        <div
          v-if="
            !selectedType ||
            selectedType === 'scissors' ||
            !oponentSelectedType ||
            oponentSelectedType === 'scissors'
          "
          class="game__body scissors"
          data-type="scissors"
        >
          <button class="game__body-item" @click="handleClick('scissors')">
            <img src="../../assets/icon-scissors.svg" alt="scissors" />
          </button>
        </div>
        <div
          v-if="!selectedType || selectedType === 'rock'"
          class="game__body"
          data-type="rock"
        >
          <button class="game__body-item" @click="handleClick('rock')">
            <img src="../../assets/icon-rock.svg" alt="rock" />
          </button>
        </div>
      </transition-group>
    </div>
  </transition>

  <transition name="fade">
    <div class="game__picked" v-if="selectedType">
      <div class="game__picked-wrapper">
        <div class="game__picked-your">
          <div class="game__picked-title">YOU PICKED</div>
          <div :class="[`game__body game__body-large ${selectedType}`]">
            <button class="game__body-item game__item-large">
              <img
                class="game__img-large"
                :src="getSelectedImage"
                :alt="selectedType"
              />
            </button>
            <div v-if="playerWin">
              <CircleAnimation />
            </div>
          </div>
        </div>

        <div v-if="oponentSelectedType" class="game__result">
          <div class="game__result-title">{{ gameResultTitle }}</div>
          <button @click="restartGame" class="game__result-button">
            PLAY AGAIN
          </button>
        </div>
        <div v-if="oponentSelectedType" class="game__picked-oponent">
          <div class="game__picked-title">THE HOUSE PICKED</div>
          <div :class="[`game__body game__body-large ${oponentSelectedType}`]">
            <button class="game__body-item game__item-large">
              <img
                class="game__img-large"
                :src="randomItem"
                :alt="oponentSelectedType"
              />
            </button>
            <div v-if="computerWin">
              <CircleAnimation />
            </div>
          </div>
        </div>
        <div class="game__wait" v-else>
          <div class="game__picked-title">THE HOUSE PICKED</div>
          <div class="game__wait-body"></div>
        </div>
      </div>
    </div>
  </transition>
</template>

<script>
import paper from "../../assets/icon-paper.svg";
import scissors from "../../assets/icon-scissors.svg";
import rock from "../../assets/icon-rock.svg";
import CircleAnimation from "../CircleAnimation.vue";

export default {
  name: "Game",
  components: {
    CircleAnimation,
  },
  data() {
    return {
      selectedType: null,
      opponentPick: [paper, scissors, rock],
      oponentSelectedType: null,
      gameResultTitle: "",
      winCounter: 0,
      randomItem: null,
      playerWin: false,
      computerWin: false,
      winConditions: {
        rock: "scissors",
        paper: "rock",
        scissors: "paper",
      },
    };
  },
  computed: {
    getSelectedImage() {
      switch (this.selectedType) {
        case "paper":
          return paper;
        case "scissors":
          return scissors;
        case "rock":
          return rock;
        default:
          return "";
      }
    },
  },
  methods: {
    handleClick(type) {
      this.selectedType = type;

      setTimeout(() => {
        this.randomItem = this.getOpponentPick();
        this.getGameResult();
      }, 2000);
    },
    getOpponentPick() {
      const randomItem =
        this.opponentPick[Math.floor(Math.random() * this.opponentPick.length)];
      this.randomItem = randomItem;
      this.oponentSelectedType = randomItem.split("icon-")[1].split(".svg")[0];
      return randomItem;
    },
    getGameResult() {
      if (this.selectedType === this.oponentSelectedType) {
        this.gameResultTitle = "DRAW";
      } else if (
        this.winConditions[this.selectedType] === this.oponentSelectedType
      ) {
        this.gameResultTitle = "YOU WIN";
        this.playerWin = true;
        this.incrementWinCounter();
      } else {
        this.computerWin = true;
        this.gameResultTitle = "YOU LOST";
        this.computerWin = true;
      }
    },
    incrementWinCounter() {
      this.winCounter++;
      this.$emit("updateWinCounter", this.winCounter);
    },
    restartGame() {
      this.selectedType = null;
      this.oponentSelectedType = null;
      this.gameResultTitle = "";
      this.randomItem = null;
      this.playerWin = false;
      this.computerWin = false;
    },
  },
};
</script>

<style lang="scss">
@import "../../variables";
/* Стили для fade transition */
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s;
}
.fade-enter, .fade-leave-to /* .fade-leave-active до версии 2.1.8 */ {
  opacity: 0;
}

/* Стили для slide transition */
.slide-enter-active,
.slide-leave-active {
  transition: all 0.5s;
}
.slide-enter, .slide-leave-to /* .slide-leave-active до версии 2.1.8 */ {
  transform: translateY(30px);
  opacity: 0;
}
.game {
  margin: 0 auto;
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
  width: 500px;
  margin-top: 64px;
  gap: 80px;
  &__active {
    display: none;
  }
  &__img {
    &-large {
      width: 88px;
      height: 118px;
      object-fit: contain;
    }
  }
  &__wait {
    &-body {
      width: 224.63px;
      height: 224.63px;
      background: rgba(0, 0, 0, 0.1);
      border-radius: 100%;
    }
  }
  &__body {
    &-large {
      width: 292.61px !important;
      height: 300px !important;
    }
  }

  &__item {
    &-large {
      width: 244.88px !important;
      height: 244.88px !important;
    }
  }
  &__result {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    &-title {
      color: rgb(255, 255, 255);
      font-family: $barlow;
      font-size: 56px;
      font-weight: 700;
      line-height: 67px;
      letter-spacing: 0px;
      text-align: center;
      margin-bottom: 16px;
    }

    &-button {
      width: 220px;
      height: 48px;
      border-radius: 8px;

      box-shadow: 0px 3px 3px 0px rgba(0, 0, 0, 0.2);
      background: linear-gradient(
        0deg,
        rgb(243, 243, 243),
        rgb(255, 255, 255) 100%
      );
      border: none;
      color: rgb(59, 66, 98);
      font-family: $barlow;
      font-size: 16px;
      font-weight: 600;
      line-height: 19px;
      letter-spacing: 2.5px;
      z-index: 20;
      cursor: pointer;
    }
    &-button:hover {
      color: rgb(219, 46, 77);
    }
  }
  &__picked {
    display: block;
    &-title {
      margin-bottom: 63px;
      color: rgb(255, 255, 255);
      font-family: $barlow;
      font-size: 24px;
      font-weight: 700;
      line-height: 32px;
      letter-spacing: 3px;
    }
    &-wrapper {
      display: flex;
      justify-content: center;
      gap: 72px;
      margin-top: 72px;
    }
  }
  &__not-picked {
    display: none;
  }
  &__triangle {
    position: absolute;
    z-index: -1;
    top: 20em;
  }
  &__body:hover::after {
    content: "";
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    width: 0;
    height: 0;
    border-radius: 50%;
    background: rgb(255, 255, 255);
    opacity: 0.05;

    opacity: 0;
    transition: width 0.3s ease, height 0.3s ease, opacity 0.3s ease;
    z-index: -1;
  }
  &__body:hover::after {
    width: 250px;
    height: 250px;
    opacity: 0.5;
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
