<template>
  <Loader v-if="ready" />
  <div class="card">
    <h3 @click="loadInformation">{{ name }}</h3>
    <div class="circle" @click="addFavorite">
      <i
        class="fas fa-star"
        v-bind:style="{ color: favorite ? '#ECA539' : '#BFBFBF' }"
      ></i>
    </div>
  </div>
</template>


<script>
import axios from "axios";
import Loader from "@/components/Loader.vue";

export default {
  name: "ItemCard",
  props: {
    name: String,
    informationUrl: String,
    favorite: {
      type: Boolean,
      default: false,
    },
    index: Number,
  },
  components: {
    Loader,
  },
  emits: ["action"],
  data() {
    return {
      pokemonInfo: {
        imgUrl: String,
        name: String,
        height: String,
        weight: String,
        types: String,
      },
      ready: false,
    };
  },
  computed: {
    getTypes() {
      return this.pokemonInfo.types.map((t) => ` ${t.type.name}`);
    },
  },
  methods: {
    openModal() {
      this.$swal.fire({
        html: `<div style="width: 100%; height: 300px; background-image: url(https://www.skyservants.com/pokemon-bg.png); background-size: cover; display: flex; justify-content: center; align-items: center; border-top-left-radius: 5px; border-top-right-radius: 5px; box-sizing: border-box">
          <img src="${
            this.pokemonInfo.imgUrl
          }" alt="poke-img" style="height: 70%; animation: floating 3s infinite ease-in-out;">
        </div>
        <div style="margin: 25px 50px; text-align: left">
        <h4 style="font-weight: bold; color: #5E5E5E; padding: 15px 0; text-transform: capitalize;">Name: <span style="">${
          this.pokemonInfo.name
        }</span></h4>
        <hr style="background-color: #E8E8E8; border: none; height: 2px">
        <h4 style="font-weight: bold; color: #5E5E5E; padding: 15px 0">Weight: <span style="">${
          this.pokemonInfo.weight
        }</span></h4>
        <hr style="background-color: #E8E8E8; border: none; height: 2px">
        <h4 style="font-weight: bold; color: #5E5E5E; padding: 15px 0">Height: <span style="">${
          this.pokemonInfo.height
        }</span></h4>
        <hr style="background-color: #E8E8E8; border: none; height: 2px">
        <h4 style="font-weight: bold; color: #5E5E5E; padding: 15px 0; text-transform: capitalize;">Types: <span style="">${
          this.getTypes
        }</span></h4>
        <hr style="background-color: #E8E8E8; border: none; height: 2px">
        </div> 
        <div style="margin: 0 50px; display: flex; flex-flow: row nowrap; justify-content: space-between; align-items: center; margin-bottom: 30px">
        <button style="width: auto; background-color: #F22539; padding: 0 10px">Share to my friends</button>
        <div style="width: 44px; height: 44px; background-color: #F5F5F5; display: flex; justify-content: center; align-items: center; margin-left: 20px; border-radius: 50%; cursor: pointer">
        <i class="fas fa-star" style="font-size: 22px; color: ${
          this.favorite ? "#ECA539" : "#BFBFBF"
        }"></i>
        </div>
        </div>
        `,
        padding: 0,
        showCloseButton: true,
        showCancelButton: false,
        showConfirmButton: false,
      });
    },
    loadInformation() {
      this.ready = true;
      axios
        .get(this.informationUrl)
        .then((res) => {
          const {
            data,
            data: { types },
          } = res;
          this.pokemonInfo.name = data.name;
          this.pokemonInfo.height = data.height;
          this.pokemonInfo.weight = data.weight;
          this.pokemonInfo.imgUrl =
            data.sprites.other.dream_world.front_default;
          this.pokemonInfo.types = types;
          setTimeout(() => {
            this.ready = false;
            this.openModal();
          }, 500);
        })
        .catch((err) => {
          this.ready = false;
          console.log(err);
        });
    },
    addFavorite() {
      this.$emit("action", {
        name: this.name,
        url: this.informationUrl,
        index: this.index,
      });
      this.$swal.fire({
        html: `
          <div>
            <h2 style="color: green"><i class="fas fa-check"></i> Done!</h2>
            <h4 style="color: #353535">Pokemon added to favorites.</h4>
          </div>
        `,
        timer: 1500,
        timerProgressBar: true,
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
  margin: 10px 0;
  padding: 0 20px;
  width: 100%;

  h3 {
    cursor: pointer;
    width: 100%;
    text-transform: capitalize;
  }

  .circle {
    @include flex-center;
    background-color: $color-lightwhite;
    border-radius: 50%;
    cursor: pointer;
    height: 44px;
    width: 44px;

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