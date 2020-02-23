<template>
  <div id="app">
    <ul>
      <li v-for="region in regionList" :key="region.name">
        <button @click="displayRegionFct(region)">{{region.name}}</button>
      </li>
    </ul>

    <region v-show="displayRegion"
            :name="displayRegion.name"
            :wine-list="displayRegion.wineList"
            :cheese-list="displayRegion.cheeseList"></region>

    <button @click="displayFormFct">Create new region</button>
    <create-region v-if="displayForm" v-on:add-new-region="updateRegionList"></create-region>
  </div>
</template>

<script>
import Region from './components/Region.vue'
import CreateRegion from './components/CreateRegion.vue'

export default {
  name: 'App',

  components: {
    Region,
    CreateRegion,
  },

  data() {
    return {
      regionList: [
        {
          name: 'Région 11',
          wineList: ['Vin 1', 'Vin 1.1', 'Vin 1.2'],
          cheeseList: ['Fromage 1']
        },
        {
          name: 'Région 2',
          wineList: ['Vin 2'],
          cheeseList: ['Fromage 2', 'Fromage 2.1', 'Fromage 2.2']
        },
        {
          name: 'Région 3',
          wineList: ['Vin 3'],
          cheeseList: ['Fromage 3']
        }
      ],
      displayRegion: false,
      displayForm: false
    }
  },

  methods: {
    displayRegionFct(region) {
      this.displayRegion = region;
    },

    updateRegionList(updateRegion) {
      this.regionList.push(updateRegion);
      this.displayForm = false;
    },

    displayFormFct() {
      this.displayForm = true;
    }
  }
}
</script>

<style>
</style>
