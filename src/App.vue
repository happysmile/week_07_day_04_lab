<template>
  <div id="app">
    <h1>Brewdog</h1>
    <beers-list v-bind:beers="beers"></beers-list>
    <section>
      <beer-details v-if="selectedBeer" v-bind:beer="selectedBeer"></beer-details>
      <favourite-beers-list v-if="favouriteBeers.length>0" v-bind:favouriteBeers="favouriteBeers"></favourite-beers-list>
    </section>
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

    for(let i=1; i<=5; i++){
      this.promises.push("https://api.punkapi.com/v2/beers?page="+i+"&per_page=80")
    };

    for(let promise of this.promises){
      fetch(promise)
      .then(results => results.json())
      .then(results => this.beers.push(results))
      .then(() => this.beers = this.beers.flat());
    }

    // fetch('https://api.punkapi.com/v2/beers')
    // .then(results => results.json())
    // .then(results => this.beers = results);

    eventBus.$on('beer-selected', (beer)=>{ this.selectedBeer = beer;});
    eventBus.$on('beer-favourite', (beer) => {
      if(!this.favouriteBeers.includes(beer)){
        this.favouriteBeers.push(beer);
      }
    });
    eventBus.$on('beer-non-favourite', (beer) => {
      const beerIndex = this.favouriteBeers.indexOf(beer)
      this.favouriteBeers.splice(beerIndex,1)
    })
  }
}
</script>

<style>
#app {
  position: relative;
  font-family: Verdana, Arial, sans-serif;
}
#app section {
  position: fixed;
  right: 0;
  top: 0;
  display: flex;
}
ul {
  padding: 0;
  list-style: none;
}
</style>
