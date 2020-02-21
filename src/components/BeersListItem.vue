<template lang="html">
  <li v-bind:class="{ favourite : isFavourite }">
    <h2 v-on:click="showDetails" v-bind:class="{ showing : isShowing }">{{beer.name}}</h2>
    <button v-if="isFavourite" v-on:click="removeFromFavourites">Remove from favourites</button>
    <button v-if="!isFavourite" v-on:click="addToFavourites">Add to favourites</button>
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
  props: ['beer', 'isShowing'],
  methods: {
    showDetails(){
      this.showingDetails = true;
      eventBus.$emit('beer-selected', this.beer);
    },
    addToFavourites(){
      this.isFavourite = true;
      eventBus.$emit('beer-favourite', this.beer);
    },
    removeFromFavourites(){
      this.isFavourite = false;
      eventBus.$emit('beer-non-favourite', this.beer);
    }
  }
}
</script>

<style lang="css" scoped>
li.favourite {
  background-color: pink;
}
h2.showing {
  color: darkgrey;
}
li {
  border-bottom: 1px solid 	lavender;
  padding: 10px;
  margin: 0px;
}
button {
  border: 1px purple solid;
  background-color: white;
  color: purple;
  display: block;
  margin: auto;
}

</style>
