<template>
  <div>
    <transition name="fade">
      <div v-if="rulesActive" class="overlay"></div>
    </transition>

    <transition name="fade">
      <div v-if="rulesActive" class="rules__modal">
        <div class="rules__modal-header">
          <div class="rules__modal-title">RULES</div>
          <button @click="toggleRules" class="rules__button-close">
            <img
              class="rules__close"
              src="../../assets/icon-close.svg"
              alt="iconClose"
            />
          </button>
        </div>

        <div class="rules__modal-img">
          <img src="../../assets/image-rules.svg" alt="rules" />
        </div>

        <button @click="toggleRules" class="adaptive">
          <img
            class="rules__close"
            src="../../assets/icon-close.svg"
            alt="iconClose"
          />
        </button>
      </div>
    </transition>

    <button class="rules" @click="toggleRules">RULES</button>
  </div>
</template>

<script>
export default {
  name: "Rules",
  data() {
    return {
      rulesActive: false,
    };
  },
  methods: {
    toggleRules() {
      this.rulesActive = !this.rulesActive;
    },
  },
};
</script>

<style lang="scss">
@import "../../variables";
.adaptive {
  display: none;
}
.overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.5);
  z-index: 998;
}

.rules:hover {
  background-color: white;
  color: rgb(59, 66, 98);
}

.rules {
  position: absolute;
  right: 32px;
  bottom: 32px;
  width: 128px;
  height: 40px;
  border: 1px solid rgb(255, 255, 255);
  border-radius: 8px;
  background: none;
  color: rgb(255, 255, 255);
  font-family: $barlow;
  font-size: 16px;
  font-weight: 600;
  line-height: 19px;
  letter-spacing: 2.5px;
  text-align: center;

  &__close {
    width: 22.09px;
    height: 22.09px;
    margin-top: 38px;
    margin-right: 31.91px;
  }

  &__button {
    &-close {
      border: none;
      background-color: none;
      background: none;
      padding: 0;
      cursor: pointer;
      display: block;
    }
  }

  &__modal {
    position: absolute;
    right: 50%;
    top: -5rem;
    transform: translate(50%, 50%);
    width: 400px;
    height: 415px;
    border-radius: 8px;
    box-shadow: 0px 3px 3px 0px rgba(0, 0, 0, 0.2);
    background: rgb(255, 255, 255);
    z-index: 999;

    &-img {
      margin-top: 48px;
    }

    &-title {
      margin-top: 32px;
      margin-left: 32px;
      color: rgb(59, 66, 98);
      font-family: $barlow;
      font-size: 32px;
      font-weight: 700;
      line-height: 32px;
      letter-spacing: 0px;
      text-align: left;
    }

    &-header {
      display: flex;
      justify-content: space-between;
    }
  }
}

@media screen and (max-width: 800px) {
  .rules {
    position: unset;
    margin-top: 139px;
  }
}

/* Animation Styles */
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s;
}

.fade-enter, .fade-leave-to /* .fade-leave-active in <2.1.8 */ {
  opacity: 0;
}

@media screen and (max-width: 450px) {
  .adaptive {
    display: block;
    border: none !important;
    background: none !important;
    padding: 0;
    margin: 0 auto;
  }
  .rules {
    &__modal {
      top: -24rem;
      position: absolute;

      width: 100vw;
      height: 120vh;
      z-index: 999;
      background-color: white;

      &-title {
        margin: 0 auto;

        margin-top: 95px;

        margin-bottom: 53px;
      }
    }
    &__close {
      margin: 0;
      margin-top: 104px;
    }
    &__button {
      &-close {
        display: none;
      }
    }
  }
}
</style>
