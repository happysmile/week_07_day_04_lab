<template lang="html">
  <li v-on:click="showDetails">
    <h2>{{beer.name}}</h2>
    <img v-bind:src="beer.image_url" v-bind:alt="beer.name" height="200">
  </li>
</template>

<script>

import {eventBus} from '../main.js';

export default {
  name: 'beers-list-item',
  props: ['beer'],
  methods: {
    showDetails(){
      eventBus.$emit('beer-selected', this.beer)
    }
  }
}
</script>

<style lang="css" scoped>
</style>
