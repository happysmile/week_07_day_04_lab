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
    padding: 10px;
    background-color: seashell;
    border: 1px purple solid;
    border-radius: 15px;
    width: 300px;
    height: 500px;
    overflow: auto;
    position: absolute;
    top: 0;
    left: 0;
  }
  li {
    padding: 10px;
  }
  li:nth-child(even){
    background-color: white;
  }
</style>
