<template>
  <button class="rules">RULES</button>
</template>

<script>
export default {
  name: "Rules",
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
}
</style>
