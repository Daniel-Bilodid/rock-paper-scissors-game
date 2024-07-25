<template>
  <div class="game" v-if="!selectedType">
    <div class="game__triangle">
      <img src="../../assets/bg-triangle.svg" alt="triangle" />
    </div>
    <div class="game__body paper" data-type="paper">
      <button class="game__body-item" @click="handleClick">
        <img src="../../assets/icon-paper.svg" alt="paper" />
      </button>
    </div>

    <div class="game__body scissors" data-type="scissors">
      <button class="game__body-item" @click="handleClick">
        <img src="../../assets/icon-scissors.svg" alt="scissors" />
      </button>
    </div>
    <div class="game__body" data-type="rock">
      <button class="game__body-item" @click="handleClick">
        <img src="../../assets/icon-rock.svg" alt="rock" />
      </button>
    </div>
  </div>

  <div class="game__picked" v-if="selectedType">
    <div class="game__picked-wrapper">
      <div class="game__picked-your">
        <div class="game__picked-title">YOU PICKED</div>
        <div :class="[`game__body ${selectedType}`]">
          <button class="game__body-item">
            <img :src="getSelectedImage" :alt="selectedType" />
          </button>
        </div>
      </div>

      <div class="game__result">
        <div class="game__result-title">{{ gameResultTitle }}</div>
        <button class="game__result-button">PLAY AGAIN</button>
      </div>
      <div v-if="oponentSelectedType" class="game__picked-oponent">
        <div class="game__picked-title">THE HOUSE PICKED</div>
        <div :class="[`game__body ${oponentSelectedType}`]">
          <button class="game__body-item">
            <img :src="getOpponentPick" :alt="getOpponentPick" />
          </button>
        </div>
      </div>
      <div class="game__wait" v-else>
        <div class="game__picked-title">THE HOUSE PICKED</div>
        <div class="game__Wait-body"></div>
      </div>
    </div>
  </div>
</template>

<script>
import paper from "../../assets/icon-paper.svg";
import scissors from "../../assets/icon-scissors.svg";
import rock from "../../assets/icon-rock.svg";

export default {
  name: "Game",
  data() {
    return {
      selectedType: null,
      opponentPick: [paper, scissors, rock],
      oponentSelectedType: null,
      gameResultTitle: "",
      winCounter: 0,
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
    getOpponentPick() {
      let randomItem =
        this.opponentPick[Math.floor(Math.random() * this.opponentPick.length)];
      let oponentSelectedType = randomItem.split("icon-")[1].split(".svg")[0];

      this.oponentSelectedType = oponentSelectedType;
      return randomItem;
    },
    getGameResult() {
      console.log("meow");
      if (this.selectedType === this.oponentSelectedType) {
        this.gameResultTitle = "DRAW";
      } else if (
        this.winConditions[this.selectedType] === this.oponentSelectedType
      ) {
        this.gameResultTitle = "YOU WIN";
      } else {
        this.gameResultTitle = "YOU LOST";
      }
      return this.gameResultTitle;
    },
  },
  methods: {
    handleClick(event) {
      const bodyElement = event.target.closest(".game__body");
      const type = bodyElement ? bodyElement.getAttribute("data-type") : null;
      this.selectedType = type;
      setTimeout(() => {
        this.getOpponentPick;
        this.getGameResult;
      }, 2000);
    },
  },
};
</script>

<style lang="scss">
@import "../../variables";
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
  &__wait {
    &-body {
      width: 224.63px;
      height: 224.63px;
      background: rgba(0, 0, 0, 0.1);
      border-radius: 100%;
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
