<template>
  <div class="main-empty">
    <h1>Uh-oh!</h1>
    <p>You look lost on your journey!</p>
    <button @click="goToWelcome">Go back home</button>
  </div>
</template>

<script>
export default {
  name: "Empty",
  methods: {
    goToWelcome() {
      this.$router.push("/");
    },
  },
};
</script>

<style lang="scss" scoped>
@import "../styles/main.scss";

.main-empty {
  @include flex-center;
  flex-flow: column nowrap;
  margin-top: 30px;

  & > *:not(:last-child) {
    margin-bottom: 25px;
  }
  button {
    @include orange-button;
  }
}
</style>