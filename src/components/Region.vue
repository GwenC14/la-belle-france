<template>
    <div class="region">
      <h2>{{name}}</h2>
      <p>Vins :</p>
      <ul>
        <li v-for="wine in wineList" :key="wine">{{wine}}</li>
      </ul>
      <p>Fromages : </p>
      <ul>
        <li v-for="cheese in cheeseList" :key="cheese">{{cheese}}</li>
      </ul>
    </div>
</template>

<script>
export default {
  name: 'Region',
  props: {
    name: String,
    wineList: Array,
    cheeseList: Array,
  }
}
</script>

<style scoped>
</style>
