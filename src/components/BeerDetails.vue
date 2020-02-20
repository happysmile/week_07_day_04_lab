<template lang="html">
  <div class="beer-details">
    <h2>{{beer.name}}</h2>
    <img v-bind:src="beer.image_url" v-bind:alt="beer.name" height="200">
    <p>ABV {{beer.abv}}%</p>
    <p>{{beer.description}}</p>
    <p>Firstly brewed: {{beer.first_brewed}}</p>
    <p>Great with:</p>
    <ul>
      <li v-for="food of beer.food_pairing">{{food}}</li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "beer-details",
  props: ["beer"]
}
</script>

<style lang="css" scoped>
.beer-details {
  padding: 10px;
  background-color: seashell;
  border: 1px purple solid;
  border-radius: 15px;
  width: 300px;
  height: 500px;
  overflow: auto;
  position: absolute;
  top: 0;
  right: 0;
}
img {
  margin: 10px auto 0 auto;
  display: block;
}
</style>
