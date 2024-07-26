<template>
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
  </div>
  <button class="rules" @click="toggleRules">RULES</button>
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
    }
  }
  &__modal {
    position: absolute;
    right: 50%;
    top: 5%;
    transform: translate(50%, 50%);
    width: 400px;
    height: 415px;
    border-radius: 8px;

    box-shadow: 0px 3px 3px 0px rgba(0, 0, 0, 0.2);
    background: rgb(255, 255, 255);
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
</style>
