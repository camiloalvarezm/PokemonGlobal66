<template>
  <div class="loader-container">
    <img src="../assets/img/loader.svg" alt="img-loader" />
  </div>
</template>

<script>
export default {
  name: "Loader",
};
</script>

<style lang="scss" scoped>
@import "../styles/main.scss";

.loader-container {
  @include flex-center;
  background-color: white;
  height: 100vh;
  opacity: .92;
  position: absolute;
  width: 100%;
  z-index: 100;

  img {
    animation: rotation 1.2s infinite linear;
    opacity: 1;
  }
}

@keyframes rotation {
  from {
    transform: rotate(0deg);
  }
  to {
    transform: rotate(359deg);
  }
}
</style>