<template>
  <div class="row">
  <div class="col-md-8">
    <grid :code="code"></grid>
  </div>
  <div class="col-md-4">
    <h2> Colors</h2>
    <div>
    <div id='blue' v-active="" :style="{ backgroundColor:'#44BEED' }" class="item" @click="selectedColor='blue'">
    </div>

    <div :style="{ backgroundColor: '#89E02B' }" :class="['item-fn', {'on': selectedColor == 'green'}]" @click="selectedColor='green'">
    </div>

    <div :style="{ backgroundColor:'#FD9B28' }" :class="['item-fn', {'on': selectedColor == 'red'}]" @click="selectedColor='red'">
    </div>
    <div :style="{ backgroundColor:'#ECECEC' }" :class="['item-fn', {'on': selectedColor == 'grey'}]" @click="selectedColor='grey'">
    </div>
      <br />
      <br />
    </div>
    <h2> Arrows</h2>
    <div>
      <table>
        <tr>
      <td  :class="['item-fn', {'on': selectedSign == 'turnLeft'}]" @click="selectedSign='turnLeft'">
        <img :src="signSources['turnLeft']">
      </td>
      <td  :class="['item-fn', {'on': selectedSign == 'turnRight'}]" @click="selectedSign='turnRight'">
        <img :src="signSources['turnRight']"></td>

      <td  :class="['item-fn', {'on': selectedSign == 'straight'}]" @click="selectedSign='straight'">
        <img :src="signSources['straight']"></td>
      <td  :class="['item-fn', {'on': selectedSign == 'f1'}]" @click="selectedSign='f1'">
        F1
      </td>
        <div :class="['item-fn', {'on': selectedSign == 'f2'}]" @click="selectedSign='f2'">
          F2
        </div>
        </tr>
      </table>
    </div>
    <br />
    <br />
    <br />
    <table>
   <tr v-for="(funcCode,funcName) in code">
     <td><h2>{{ funcName }}</h2></td>
      <td v-for="(elem, i) in funcCode" v-bind:style="{ backgroundColor: getColorItem(elem) }" class="item-fn" @click="change(elem)">
        <img v-if="getSign(elem)" :src="getSign(elem)">
        <h2 v-else> {{ elem.sign }} </h2>
      </td>
    <br />
    <br />
    <br />
  </tr>
    </table>
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
        f1: [{color: 'grey', sign: 'straight'}, {color: 'blue', sign: 'f1'}, {color: 'grey', sign: 'f2'}],
        f2: [{color: 'grey', sign: 'straight'}, {color: 'grey', sign: 'turnLeft'}, {color: 'grey', sign: 'straight'}, {color: 'grey', sign: 'turnRight'}]
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
.on {
  border: 2px solid black;
}
</style>
