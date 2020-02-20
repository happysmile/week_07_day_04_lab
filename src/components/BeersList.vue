<template lang="html">
  <ul v-if="beers">
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
</style>
