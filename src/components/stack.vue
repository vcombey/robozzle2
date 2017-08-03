<template>
  <div>
  <div v-for="elem in stack.slice(0,20)" v-bind:style="{ backgroundColor: getColorItem(elem) }" class="item">
    <img v-if="getSign(elem)" :src="getSign(elem)">
    <h2 v-else> {{ elem.sign }} </h2>
  </div>
  </div>
</template>

<script>
  import { colorSign } from './mixinColorSign.js'
  export default {
    props: ['stack'],
    mixins: [colorSign]
  }
</script>

<style>
  .item {
    width: 35px;
    height: 35px;
    float: left;
    background-color: grey;
    border: 1px solid white;
  }
</style>
