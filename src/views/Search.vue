<template>
  <div class="main-search">
    <div class="search-container">
      <div class="search-input">
        <i class="fas fa-search"></i>
        <input class="input-field" type="text" />
      </div>
    </div>
    <Empty />
  </div>
</template>

<script>
import Empty from "@/components/Empty.vue";

export default {
  name: "Search",
  components: {
    Empty,
  },
};
</script>

<style lang="scss" scoped>
@import "../styles/main.scss";

.main-search {
  margin: 35px 30px;

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
}

@media (min-width: 768px) {

    .search-input {
        width: 570px;
        margin-left: auto;
        margin-right: auto;
    }
}
</style>