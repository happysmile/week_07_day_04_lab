<template lang="html">
  <li v-bind:class="{ favourite : isFavourite }">
    <h2 v-on:click="showDetails">{{beer.name}}</h2>
    <img v-on:click="showDetails" v-bind:src="beer.image_url" v-bind:alt="beer.name" height="200">
    <button v-if="!isFavourite" v-on:click="addToFavourites">Add to favourites</button>
    <button v-if="isFavourite" v-on:click="removeFromFavourites">Remove from favourites</button>
  </li>
</template>

<script>

import {eventBus} from '../main.js';

export default {
  name: 'beers-list-item',
  data(){
    return {
      isFavourite: false
    }
  },
  props: ['beer'],
  methods: {
    showDetails(){
      eventBus.$emit('beer-selected', this.beer)
    },
    addToFavourites(){
      this.isFavourite = true;
      eventBus.$emit('beer-favourite', this.beer)
    },
    removeFromFavourites(){
      this.isFavourite = false;
      eventBus.$emit('beer-non-favourite', this.beer)
    }
  }
}
</script>

<style lang="css" scoped>
.favourite {
  background-color: pink;
}
</style>
