<template lang="html">
  <ul id="beers-list" v-if="beers">
    <beers-list-item v-for="(beer, index) in beers" v-bind:key="index" v-bind:beer="beer"></beers-list-item>
  </ul>
</template>

<script>
import BeersListItem from './BeersListItem.vue';
export default {
  name: "beers-list",
  props: ['beers'],
  components: {
    "beers-list-item" : BeersListItem
  }
}
</script>

<style lang="css" scoped>
 #beers-list {
   background-color: white;
   border: 1px purple solid;
   width: 500px;
   height: 500px;
   overflow: auto;
   margin: auto;
 }
</style>
