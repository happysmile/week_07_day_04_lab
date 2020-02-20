<template lang="html">
  <div class="beer-details">
    <h2>{{beer.name}}</h2>
    <img v-bind:src="beer.image_url" v-bind:alt="beer.name" height="200">
    <p>ABV {{beer.abv}}%</p>
    <p>{{beer.description}}</p>
    <p>Firstly brewed: {{beer.firstly_brewed}}</p>
    <p>Great with:</p>
    <ul>
      <li v-for="food of beer.food_pairing">{{food}}</li>
    </ul>
    <p>Brewer tips: {{beer.brewers_tips}}</p>
  </div>
</template>

<script>
export default {
  name: "beer-details",
  props: ["beer"]
}
</script>

<style lang="css" scoped>
</style>
