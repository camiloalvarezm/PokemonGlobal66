<template>
  <Loader v-if="ready" />
  <div class="main-search animate__animated animate__fadeIn" v-if="!ready">
    <div class="search-container">
      <div class="search-input">
        <i class="fas fa-search"></i>
        <input
          class="input-field"
          type="text"
          placeholder="Search"
          @keypress="loadPokemons($event.target.value)"
        />
      </div>
    </div>
    <Empty class="empty" v-if="pokemonList.length === 0" />
    <div v-for="(pokemon, index) in pokemonList" :key="index">
      <ItemCard
        :name="pokemon.name"
        :informationUrl="pokemon.url"
        :favorite="pokemon.favorite"
        :index="index"
        @action="addToFavorites($event)"
      />
    </div>
  </div>

  <div class="navbar">
    <div class="actions">
      <button
        @click="loadAll"
        v-bind:class="{ active: allSelected, disabled: !allSelected }"
      >
        <i class="fas fa-list"></i> All
      </button>
      <button
        @click="loadFavorites"
        v-bind:class="{
          active: favoritesSelected,
          disabled: !favoritesSelected,
        }"
      >
        <i class="fas fa-star"></i> Favorites
      </button>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Empty from "@/components/Empty.vue";
import ItemCard from "@/components/ItemCard.vue";
import Loader from "@/components/Loader.vue";

export default {
  name: "Search",
  components: {
    Empty,
    ItemCard,
    Loader,
  },
  data() {
    return {
      allSelected: true,
      favoritesSelected: false,
      pokemonList: [],
      ready: true,
    };
  },
  methods: {
    loadPokemons(text) {
      axios
        .get("https://pokeapi.co/api/v2/pokemon")
        .then((res) => {
          const { data } = res;
          for (let r of data.results) {
            r.favorite = false;
          }
          this.pokemonList = [];
          if (text) {
            for (let p of data.results) {
              if (p.name.includes(text.toLowerCase())) {
                this.pokemonList.push(p);
              }
            }
            return;
          }
          this.pokemonList = data.results;
        })
        .catch((err) => console.log(err));
    },
    loadAll() {
      if (this.allSelected) {
        return;
      }
      this.allSelected = !this.allSelected;
      this.favoritesSelected = !this.favoritesSelected;
      this.loadPokemons();
      let favoritesList = localStorage.getItem("favorites");
      if (favoritesList) {
        favoritesList = JSON.parse(favoritesList);
        for (let f of favoritesList) {
          this.pokemonList[f.index].favorite = true;
        }
      }
    },
    loadFavorites() {
      if (this.favoritesSelected) {
        return;
      }
      this.allSelected = !this.allSelected;
      this.favoritesSelected = !this.favoritesSelected;
      this.pokemonList = JSON.parse(localStorage.getItem("favorites")) || [];
    },
    addToFavorites(pokemon) {
      this.pokemonList[pokemon.index].favorite = true;
      pokemon.favorite = true;
      let favorites = localStorage.getItem("favorites");
      if (favorites) {
        favorites = JSON.parse(favorites);
        favorites.push(pokemon);
        localStorage.setItem("favorites", JSON.stringify(favorites));
        return;
      }
      favorites = [];
      favorites.push(pokemon);
      localStorage.setItem("favorites", JSON.stringify(favorites));
    },
  },
  created() {
    this.loadPokemons();
    setTimeout(() => {
      this.ready = false;
    }, 500);
  },
};
</script>

<style lang="scss" scoped>
@import "../styles/main.scss";

.main-search {
  padding: 35px 30px;
  height: calc(100vh - 155px);
  overflow-y: scroll;

  .search-container {
    margin-bottom: 30px;
    .search-input {
      display: flex;
      flex-flow: row nowrap;
      align-items: center;
      background-color: white;
      box-shadow: 0px 2px 10px rgba(0, 0, 0, 0.04);
      border-radius: 5px;

      i {
        margin: 0 15px;
        color: $color-gray;
      }

      input {
        height: 50px;
        width: 100%;
        border: none;
        font-size: 16px;
        color: $color-black;

        &:focus {
          outline: none;
        }
      }
    }
  }

  .empty {
    margin-bottom: 35px;
  }
}

.navbar {
  @include flex-center;
  background-color: white;
  bottom: 0;
  box-shadow: 0px -5px 4px rgba(0, 0, 0, 0.05);
  height: 80px;
  overflow: hidden;
  position: fixed;
  width: 100%;

  .actions {
    @include flex-center;
    justify-content: space-evenly;
    width: 570px;
  }
}

.active {
  background-color: $color-orange;
}

.disabled {
  background-color: $color-gray;
}

@media (min-width: 768px) {
  .search-input {
    width: 570px;
    margin-left: auto;
    margin-right: auto;
  }
}
</style>