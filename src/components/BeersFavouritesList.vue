<template lang="html">
  <div class="favourite-beers">
    <h2>Favourite beers</h2>
    <ul>
      <li v-for="beer in favouriteBeers">{{beer.name}}</li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "favourite-beers-list",
  props: ['favouriteBeers']
}
</script>

<style lang="css" scoped>
  .favourite-beers {
    border: 1px purple solid;
    width: 300px;
    height: 500px;
    overflow: auto;
  }
</style>
