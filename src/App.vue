<template>
  <div id="app">
    <h1>Brewdog</h1>
    <beer-details v-if="selectedBeer" v-bind:beer="selectedBeer"></beer-details>
    <beers-list v-bind:beers="beers"></beers-list>
  </div>
</template>

<script>
import BeersList from './components/BeersList.vue';
import {eventBus} from './main.js';
import BeerDetails from './components/BeerDetails.vue';

export default {
  name: 'app',
  data(){
    return {
      beers: [],
      selectedBeer: null,
      favouriteBeers: []
    }
  },
  components: {
    "beers-list": BeersList,
    "beer-details": BeerDetails
  },
  mounted() {
    fetch('https://api.punkapi.com/v2/beers')
    .then(results => results.json())
    .then(results => this.beers = results);
    eventBus.$on('beer-selected', (beer)=>{ this.selectedBeer = beer;});
  }
}
</script>

<style>

</style>
