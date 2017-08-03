<template>
    <div class="row">
      <div class="col-md-4"></div>
      <div class="col-md-8">
      <transition-group name="slide">
  <div v-for="(elem, i) in stack.slice(0,20)" v-bind:style="{ backgroundColor: getColorItem(elem) }" class="item-fn" :key="elem">
    <img v-if="getSign(elem)" :src="getSign(elem)">
    <h2 v-else> {{ elem.sign }} </h2>
  </div>
    </transition-group>
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
.slide-enter-active {
  animation: slide-in 0.2s ease-out forwards;
}
.slide-leave-active {
  animation: slide-out 0.2s ease-out forwards;
  position: absolute;
}
.slide-move {
  transition: transform 0.2s;
}
@keyframes slide-in {
  from {
    transform: translateX(0px);
  }
  to {
    transform: translateX(40px);
  }
}
@keyframes slide-out {
  from {
    transform: translateX(0px);
  }
  to {
    transform: translateX(-40px);
  }
}
</style>
