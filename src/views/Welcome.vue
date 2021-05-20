<template>
  <div class="main-welcome animate__animated animate__fadeIn">
    <div class="logo">
      <img src="../assets/img/pokemon-logo.svg" alt="pokemon" />
    </div>
    <div class="description">
      <h1>Welcome to Pokédex</h1>
      <p>
        The digital encyclopedia created by Professor Oak is an invaluable tool
        to Trainers in the Pokémon world.
      </p>
    </div>
    <div class="get-started">
      <button @click="goToSearch">Get started</button>
    </div>
  </div>
</template>

<script>


export default {
  name: "Welcome",
  methods: {
    goToSearch() {
      this.$router.push("/search");
    },
  }
};
</script>

<style lang="scss" scoped>
@import "../styles/main.scss";

.main-welcome {
  @include max-width(1200px);
  @include flex-center;
  flex-flow: column nowrap;
  justify-content: space-evenly;
  height: 100vh;
  padding: 0 30px;

  .description {
    text-align: center;

    h1 {
      margin-bottom: 30px;
    }
  }

  .get-started {
    button {
      @include orange-button;
    }
  }
}
</style>
