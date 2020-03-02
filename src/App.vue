<template>
  <div id="app">
    <div class="main-content">
      <ul class="region-list-content">
        <li class="region-list" v-for="region in regionList" :key="region.name">
          <button class="button btn-region" :class="{ active: displayRegion}"  @click="displayRegionFct(region)">{{region.name}}</button>
          <div class="arrow"></div>
        </li>
      </ul>

      <region v-show="displayRegion"
              :name="displayRegion.name"
              :wine-list="displayRegion.wineList"
              :cheese-list="displayRegion.cheeseList"></region>
    </div>

    <button class="button important create-region" @click="displayFormFct">Create new region</button>
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
      displayForm: false,
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

  h1, h2, h3, h4, h5, h6, p, ul, li, button, input, label {
    margin: 0;
    color: darkslategray;
  }

  ul {
    padding-left: 0;
  }

  li {
    list-style: none;
  }

  .button {
    font-size: 14px;
    -webkit-appearance: none;
    border: none;
    padding: 15px;
    border-radius: 23px;
    min-width: 130px;
    cursor: pointer;
  }

  .button.important {
    color: white;
    background-color: lightcoral;
  }

  .button.slim {
    min-width: auto;
    padding: 5px 15px;
  }

  .button.btn-region {
    background: linear-gradient(0.25turn, #fff, #ecf0f3 75%);
  }

  .button.btn-region.active {
    background: #ecf0f3;
  }

  .arrow {
    width: 0;
    height: 0;
    border-top: 22px solid transparent;
    border-bottom: 22px solid transparent;
    border-left: 25px solid #ecf0f3;
    margin-left: -15px;
  }

  #app {
    max-width: 1200px;
    margin: 0 auto;
  }

  .main-content {
    display: flex;
  }

  .region-list-content {
    flex: 1;
  }

  .region {
    flex: 2;
  }

  .region-list {
    display: flex;
    align-items: center;
    margin-bottom: 10px;
  }

  .create-region {
    margin-top: 15px;
  }

</style>
