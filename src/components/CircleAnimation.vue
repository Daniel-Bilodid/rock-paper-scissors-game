<template>
  <div class="wave wave1"></div>
  <div class="wave wave2"></div>
  <div class="wave wave3"></div>
</template>

<script>
export default {
  name: "CircleAnimation",
};
</script>

<style lang="scss">
.game__body {
  position: relative;
}

.wave {
  position: absolute;
  top: 50%;
  left: 50%;
  width: 100%;
  height: 100%;
  border: 20px solid rgb(255, 255, 255);
  border-radius: 50%;
  transform: translate(-50%, -50%);
  opacity: 0;
}

.wave1 {
  animation: wave 3s ease-in-out infinite;
  animation-delay: 1s;
}

.wave2 {
  animation: wave 3s ease-in-out infinite;
  animation-delay: 3s;
}

.wave3 {
  animation: wave 3s ease-in-out infinite;
  animation-delay: 4s;
}

@keyframes wave {
  0% {
    width: 100%;
    height: 100%;
    opacity: 1;
  }
  50% {
    width: 200%;
    height: 200%;
    opacity: 0;
  }
  100% {
    width: 200%;
    height: 200%;
    opacity: 0;
  }
}
</style>
