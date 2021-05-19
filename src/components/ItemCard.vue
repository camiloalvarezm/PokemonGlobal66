<template>
  <div class="card">
    <h3 @click="openModal">{{ name }}</h3>
    <div class="circle">
      <i class="fas fa-star"></i>
    </div>
  </div>
</template>


<script>
export default {
  name: "ItemCard",
  props: {
    name: String,
  },
  data() {
    return {};
  },
  methods: {
    openModal() {
      this.$swal.fire({
        html: `<div style="width: 100%; height: 300px; background-image: url(https://www.skyservants.com/pokemon-bg.png); background-size: cover; display: flex; justify-content: center; align-items: center">
          <img src="https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/1.svg" alt="poke-img" style="grid-column: 1">
        </div>
        <div style="margin: 25px 50px; text-align: left">
        <h4 style="font-weight: bold; color: #5E5E5E; padding: 15px 0">Name: <span style="">Squirtle</span></h4>
        <hr style="background-color: #E8E8E8; border: none; height: 2px">
        <h4 style="font-weight: bold; color: #5E5E5E; padding: 15px 0">Weight: <span style="">Squirtle</span></h4>
        <hr style="background-color: #E8E8E8; border: none; height: 2px">
        <h4 style="font-weight: bold; color: #5E5E5E; padding: 15px 0">Height: <span style="">Squirtle</span></h4>
        <hr style="background-color: #E8E8E8; border: none; height: 2px">
        <h4 style="font-weight: bold; color: #5E5E5E; padding: 15px 0">Types: <span style="">Squirtle</span></h4>
        <hr style="background-color: #E8E8E8; border: none; height: 2px">
        </div> 
        <div style="margin: 0 50px; display: flex; flex-flow: row nowrap; justify-content: space-between; align-items: center; margin-bottom: 30px">
        <button style="width: 100%; background-color: #F22539">Share to my friends</button>
        <div style="width: 50px; height: 44px; background-color: #F5F5F5; display: flex; justify-content: center; align-items: center; margin-left: 20px; border-radius: 50%">
        <i class="fas fa-star" style="font-size: 22px; color: #BFBFBF"></i>
        </div>
        </div>
        `,
        padding: 0,
        showCloseButton: true,
        showCancelButton: false,
        showConfirmButton: false,
      });
    },
  },
};
</script>

<style lang="scss" scoped>
@import "../styles/main.scss";

.card {
  @include flex-center;
  background-color: white;
  box-sizing: border-box;
  border-radius: 5px;
  height: 60px;
  justify-content: space-between;
  margin-bottom: 10px;
  padding: 0 20px;
  width: 100%;

  h3 {
    cursor: pointer;
    width: 100%
  }

  .circle {
    @include flex-center;
    background-color: $color-lightwhite;
    height: 44px;
    width: 44px;
    border-radius: 50%;

    i {
      font-size: 25px;
      color: $color-gray;
    }
  }
}

@media (min-width: 768px) {
  .card {
    width: 570px;
    margin-left: auto;
    margin-right: auto;
  }
}
</style>