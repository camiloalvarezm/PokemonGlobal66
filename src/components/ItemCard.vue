<template>
  <div class="card">
    <h3>{{ name }}</h3>
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
};
</script>

<style lang="scss" scoped>
@import "../styles/main.scss";

.card {
  @include flex-center;
  background-color: white;
  box-sizing: border-box;
  border-radius: 5px;
  cursor: pointer;
  height: 60px;
  justify-content: space-between;
  margin-bottom: 10px;
  padding: 0 20px;
  width: 100%;

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