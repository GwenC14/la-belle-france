<template>
    <div class="region">
      <h2>{{name}}</h2>
      <p>Vins :</p>
      <ul>
        <li v-for="wine in wineList" :key="wine">
          <img src="../assets/icon/wine.svg" alt="Wine">
          {{wine}}
        </li>
      </ul>
      <p>Fromages : </p>
      <ul>
        <li v-for="cheese in cheeseList" :key="cheese">
          <img src="../assets/icon/cheese.svg" alt="Cheese">
          {{cheese}}
        </li>
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

  .region {
    border-left: 10px solid #ecf0f3;
    padding-left: 25px;
  }

  h2 {
    color: lightcoral;
    margin-bottom: 15px;
  }

  ul {
    padding-left: 15px;
    margin-bottom: 20px;
  }

  li {
    display: flex;
    align-items: center;
    margin-bottom: 5px;
  }

  p {
    font-size: 18px;
    font-weight: 600;
    margin-bottom: 5px;
  }

  img {
    width: 25px;
    margin-right: 10px;
  }

</style>
