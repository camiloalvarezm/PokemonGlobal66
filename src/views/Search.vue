<template>
  <div class="main-search">
    <div class="search-container">
      <div class="search-input">
        <i class="fas fa-search"></i>
        <input class="input-field" type="text" placeholder="Search" />
      </div>
    </div>
    <Empty class="empty" />
    <ItemCard name="prueba" />
    <ItemCard name="prueba" />
    <ItemCard name="prueba" />
    <ItemCard name="prueba" />
    <ItemCard name="prueba" />
    <ItemCard name="prueba" />
    <ItemCard name="prueba" />
    <ItemCard name="prueba" />
    <ItemCard name="prueba" />
    <ItemCard name="prueba" />
    <ItemCard name="prueba" />
    <ItemCard name="prueba" />
    <ItemCard name="prueba" />
    <ItemCard name="prueba" />
  </div>

  <div class="navbar">
    <div class="actions">
      <!-- <button :class="{'background-color': allSelected ? 'blue' : 'black'}"><i class="fas fa-list"> All</i></button> -->
      <button><i class="fas fa-list"></i> All</button>
      <button><i class="fas fa-star"></i> Favorites</button>
    </div>
  </div>
</template>

<script>
import Empty from "@/components/Empty.vue";
import ItemCard from "@/components/ItemCard.vue";

export default {
  name: "Search",
  components: {
    Empty,
    ItemCard,
  }
};
</script>

<style lang="scss" scoped>
@import "../styles/main.scss";

.main-search {
  padding: 35px 30px;

  .search-container {
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

@media (min-width: 768px) {
  .search-input {
    width: 570px;
    margin-left: auto;
    margin-right: auto;
  }
}
</style>