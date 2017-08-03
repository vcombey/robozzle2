<template>
  <div class="row">
  <div class="col-md-8">
    <grid :code="code"></grid>
  </div>
  <div class="col-md-4">
    <h2> Colors</h2>
    <div>
    <div id='blue' v-active="" :style="{ backgroundColor:'blue' }" class="item" @click="selectedColor='blue'">
    </div>

    <div :style="{ backgroundColor:'green' }" :class="['item', {'on': selectedColor == 'green'}]" @click="selectedColor='green'">
    </div>

    <div :style="{ backgroundColor:'red' }" :class="['item', {'on': selectedColor == 'red'}]" @click="selectedColor='red'">
    </div>
    <div :style="{ backgroundColor:'grey' }" :class="['item', {'on': selectedColor == 'grey'}]" @click="selectedColor='grey'">
    </div>
      <br />
      <br />
    </div>
    <h2> Arrows</h2>
    <div>
      <div :style="{ backgroundColor:'grey' }" :class="['item', {'on': selectedSign == 'turnLeft'}]" @click="selectedSign='turnLeft'">
        <img :src="signSources['turnLeft']">
      </div>
      <div :style="{ backgroundColor:'grey' }" :class="['item', {'on': selectedSign == 'turnRight'}]" @click="selectedSign='turnRight'">
        <img :src="signSources['turnRight']"></div>

      <div :style="{ backgroundColor:'grey' }" :class="['item', {'on': selectedSign == 'straight'}]" @click="selectedSign='straight'">
        <img :src="signSources['straight']"></div>
      <div :style="{ backgroundColor:'grey' }" :class="['item', {'on': selectedSign == 'f1'}]" @click="selectedSign='f1'">
        F1
      </div>
        <div :style="{ backgroundColor:'grey' }" :class="['item', {'on': selectedSign == 'f2'}]" @click="selectedSign='f2'">
          F2
        </div>
    </div>
    <br />
    <br />
    <br />
   <div v-for="(funcCode,funcName) in code">
    <h1>{{ funcName }}</h1>
      <div v-for="(elem, i) in funcCode" v-bind:style="{ backgroundColor: getColorItem(elem) }" class="item" @click="change(elem)">
        {{ i }}
        <img v-if="getSign(elem)" :src="getSign(elem)">
        <h2 v-else> {{ elem.sign }} </h2>
      </div>
    <br />
    <br />
    <br />
  </div>
  </div>
  </div>
</template>

<script>
import Grid from './grid.vue'
import { colorSign } from './mixinColorSign.js'
export default {
  data () {
    return {
      selectedSign: null,
      selectedColor: 'grey',
      code: {
        f1: [{color: 'red', sign: 'turnLeft'}, {color: 'grey', sign: 'straight'}, {color: 'grey', sign: 'turnRight'}, {color: 'red', sign: 'turnLeft'}, {color: 'red', sign: 'turnLeft'}],
        f2: [{color: null, sign: null}, {color: null, sign: null}, {color: null, sign: null}]
      }
    }
  },
  methods: {
    changeColor (item) {
      if (this.selectedColor) {
        item.color = this.selectedColor
      }
    },
    changeArrow (item) {
      if (this.selectedSign) {
        item.sign = this.selectedSign
      }
    },
    change (item) {
      this.changeColor(item)
      this.changeArrow(item)
    }
  },
  components: {
    'grid': Grid
  },
  directives: {
    'active': {
      bind (el, binding, vnode) {
        console.log('bind')
        if (el.id === this.selectedColor) {
          el.class = 'active'
        }
      }
    }
  },
  mixins: [colorSign]
}
</script>

<style scoped>
.item {
  width: 35px;
  height: 35px;
  float: left;
  border: 1px solid white;
}
.on {
  border: 2px solid black;
}
</style>
