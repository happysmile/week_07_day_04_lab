<template>
  <div id="app">
    <h1>Brewdog Beers List</h1>
    <main>
      <beers-list v-bind:beers="beers"></beers-list>
      <beer-details v-if="selectedBeer" v-bind:beer="selectedBeer"></beer-details>
      <favourite-beers-list v-if="favouriteBeers.length>0" v-bind:favouriteBeers="favouriteBeers"></favourite-beers-list>
    </main>
  </div>
</template>

<script>
import BeersList from './components/BeersList.vue';
import {eventBus} from './main.js';
import BeerDetails from './components/BeerDetails.vue';
import BeersFavouritesList from './components/BeersFavouritesList.vue';

export default {
  name: 'app',
  data(){
    return {
      beers: [],
      selectedBeer: null,
      favouriteBeers: [],
      promises: []
    }
  },
  components: {
    "beers-list": BeersList,
    "beer-details": BeerDetails,
    "favourite-beers-list": BeersFavouritesList
  },
  mounted() {

    // fetch all the beers from the API (by default you have only 25 results)

    for(let i=1; i<=5; i++){
      this.promises.push("https://api.punkapi.com/v2/beers?page="+i+"&per_page=80")
    };

    for(let promise of this.promises){
      fetch(promise)
      .then(results => results.json())
      .then(results => this.beers.push(results))
      .then(() => this.beers = this.beers.flat());
    }

    // select a beer to display details

    eventBus.$on('beer-selected', (beer) => {
      this.selectedBeer = beer;
    });

    // add a beer to favourites

    eventBus.$on('beer-favourite', (beer) => {
      if(!this.favouriteBeers.includes(beer)){
        this.favouriteBeers.push(beer);
      }
    });

    // remove a beer from favourites

    eventBus.$on('beer-non-favourite', (beer) => {
      const beerIndex = this.favouriteBeers.indexOf(beer)
      this.favouriteBeers.splice(beerIndex,1)
    })
  }
}
</script>

<style>
html {
  box-sizing: border-box;
}
*, *:before, *:after {
  box-sizing: inherit;
}
body {
  background-image: linear-gradient(-90deg, red, yellow);
}
h1, h2 {
  margin: 0;
  text-align: center;
}
#app {
  position: relative;
  font-family: Verdana, Arial, sans-serif;
}
#app main {
  position: relative;
}
ul {
  padding: 0;
  list-style: none;
}
</style>
