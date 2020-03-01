<template>
  <div id="app">
    <BaseData v-bind:travel="travel"></BaseData>
    <ItemsList v-bind:items="items"></ItemsList>
  </div>
</template>

<script>
import BaseData from './components/travel/BaseData.vue'
import ItemsList from './components/travel/items/ItemsList.vue'

export default {
  name: 'App',
  components: {
    BaseData,
    ItemsList
  },
  data() {
    return {
      travel: {},
      items: {}
    }
  },
  methods: {
    initTravelBaseData() {
      this.$axios.get('/data/travel.json')
        .then(response => {
          this.travel = JSON.parse(JSON.stringify(response.data))
        });
    },

    initItemsData() {
      this.$axios.get('/data/items.json')
        .then(response => {
          this.items = JSON.parse(JSON.stringify(response.data))
        });
    }
  },
  created: function() {
      this.initTravelBaseData();
      this.initItemsData();
  }
}
</script>

<style>
</style>
