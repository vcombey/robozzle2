<template>
  <div>
    <grid :code="code"></grid>
    {{ code }}
    <h2> Colors</h2>
    <div>
    <div :style="{ backgroundColor:'blue' }" class="item" @click="selectedColor='blue'">
    </div>

    <div :style="{ backgroundColor:'green' }" class="item" @click="selectedColor='green'">
    </div>

    <div :style="{ backgroundColor:'red' }" class="item" @click="selectedColor='red'">
    </div>
      <br />
      <br />
    </div>
    <h2> Arrows</h2>
    <div>
      <div :style="{ backgroundColor:'grey' }" class="item" @click="selectedSign='turnLeft'">
        <img :src="signSources['turnLeft']">
      </div>
      <div :style="{ backgroundColor:'grey' }" class="item" @click="selectedSign='turnRight'">
        <img :src="signSources['turnRight']"></div>

      <div :style="{ backgroundColor:'grey' }" class="item" @click="selectedSign='straight'">
        <img :src="signSources['straight']"></div>
      <div :style="{ backgroundColor:'grey' }" class="item" @click="selectedSign='f1'">
        F1
      </div>
        <div :style="{ backgroundColor:'grey' }" class="item" @click="selectedSign='f2'">
          F2
        </div>
    </div>
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
</template>

<script>
import Grid from './grid.vue'
export default {
  data () {
    return {
      selectedSign: null,
      selectedColor: null,
      code: {
        f1: [{color: 'red', sign: 'turnLeft'}, {color: null, sign: 'straight'}, {color: null, sign: 'turnRight'}, {color: 'red', sign: 'turnLeft'}, {color: 'red', sign: 'turnLeft'}],
        f2: [{color: null, sign: null}, {color: null, sign: null}, {color: null, sign: null}]
      },
      signSources: {
        turnLeft: 'data:image/svg+xml;utf8;base64,PD94bWwgdmVyc2lvbj0iMS4wIiBlbmNvZGluZz0iaXNvLTg4NTktMSI/Pgo8IS0tIEdlbmVyYXRvcjogQWRvYmUgSWxsdXN0cmF0b3IgMTYuMC4wLCBTVkcgRXhwb3J0IFBsdWctSW4gLiBTVkcgVmVyc2lvbjogNi4wMCBCdWlsZCAwKSAgLS0+CjwhRE9DVFlQRSBzdmcgUFVCTElDICItLy9XM0MvL0RURCBTVkcgMS4xLy9FTiIgImh0dHA6Ly93d3cudzMub3JnL0dyYXBoaWNzL1NWRy8xLjEvRFREL3N2ZzExLmR0ZCI+CjxzdmcgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIiB4bWxuczp4bGluaz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94bGluayIgdmVyc2lvbj0iMS4xIiBpZD0iQ2FwYV8xIiB4PSIwcHgiIHk9IjBweCIgd2lkdGg9IjMycHgiIGhlaWdodD0iMzJweCIgdmlld0JveD0iMCAwIDQ2MC41MzEgNDYwLjUzMSIgc3R5bGU9ImVuYWJsZS1iYWNrZ3JvdW5kOm5ldyAwIDAgNDYwLjUzMSA0NjAuNTMxOyIgeG1sOnNwYWNlPSJwcmVzZXJ2ZSI+CjxnPgoJPHBhdGggZD0iTTQwMy4yNjIsMjU0LjE1NnYyMDYuMzc1aC03MC42MjhWMjU0LjE1NmMwLTMyLjI2LTguNDExLTU2LjE4Ny0yNS43MTgtNzMuMTZjLTI0LjYzNi0yNC4xNjYtNjAuOTA0LTI3LjkxOS03MS45MzQtMjguNDY5ICAgaC01MC43NDdsMjkuMDksNzMuNjQ4YzAuOTc5LDIuNDY4LDAuMTg3LDUuMjg0LTEuOTI3LDYuODhjLTIuMTE2LDEuNjA0LTUuMDQ4LDEuNTkzLTcuMTUyLTAuMDNMNTkuNTc0LDEyMS43OTcgICBjLTEuNDQ1LTEuMTI2LTIuMzA1LTIuODQtMi4zMDUtNC42NzhjMC0xLjgzNSwwLjg2LTMuNTYxLDIuMzA1LTQuNjcyTDIwNC4yNDYsMS4yMThjMS4wNjQtMC44MTksMi4zMjMtMS4yMTgsMy42LTEuMjE4ICAgYzEuMjQ3LDAsMi40OTQsMC4zODcsMy41NTIsMS4xODVjMi4xMTksMS41OTMsMi45MDUsNC40MTMsMS45MjcsNi44ODlsLTI5LjA5LDczLjY0MmwzNy40NDIsMC4xMDljMCwwLDMuNTg4LDAuMTk4LDguNTY1LDAuNjI0ICAgbC0wLjAxOC0wLjYzYzMuMTc0LTAuMDY3LDc1LjU2OC0wLjg1OSwxMjYuMTUzLDQ4Ljc2MUMzODcuNDkyLDE2MS4wOTIsNDAzLjI2MiwyMDIuNjY1LDQwMy4yNjIsMjU0LjE1NnoiIGZpbGw9IiMwMDAwMDAiLz4KPC9nPgo8Zz4KPC9nPgo8Zz4KPC9nPgo8Zz4KPC9nPgo8Zz4KPC9nPgo8Zz4KPC9nPgo8Zz4KPC9nPgo8Zz4KPC9nPgo8Zz4KPC9nPgo8Zz4KPC9nPgo8Zz4KPC9nPgo8Zz4KPC9nPgo8Zz4KPC9nPgo8Zz4KPC9nPgo8Zz4KPC9nPgo8Zz4KPC9nPgo8L3N2Zz4K',
        straight: 'data:image/svg+xml;utf8;base64,PD94bWwgdmVyc2lvbj0iMS4wIiBlbmNvZGluZz0iaXNvLTg4NTktMSI/Pgo8IS0tIEdlbmVyYXRvcjogQWRvYmUgSWxsdXN0cmF0b3IgMTYuMC4wLCBTVkcgRXhwb3J0IFBsdWctSW4gLiBTVkcgVmVyc2lvbjogNi4wMCBCdWlsZCAwKSAgLS0+CjwhRE9DVFlQRSBzdmcgUFVCTElDICItLy9XM0MvL0RURCBTVkcgMS4xLy9FTiIgImh0dHA6Ly93d3cudzMub3JnL0dyYXBoaWNzL1NWRy8xLjEvRFREL3N2ZzExLmR0ZCI+CjxzdmcgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIiB4bWxuczp4bGluaz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94bGluayIgdmVyc2lvbj0iMS4xIiBpZD0iQ2FwYV8xIiB4PSIwcHgiIHk9IjBweCIgd2lkdGg9IjMycHgiIGhlaWdodD0iMzJweCIgdmlld0JveD0iMCAwIDM0OS43NTcgMzQ5Ljc1NiIgc3R5bGU9ImVuYWJsZS1iYWNrZ3JvdW5kOm5ldyAwIDAgMzQ5Ljc1NyAzNDkuNzU2OyIgeG1sOnNwYWNlPSJwcmVzZXJ2ZSI+CjxnPgoJPGc+CgkJPGc+CgkJCTxnPgoJCQkJPHBhdGggZD0iTTI5OC4wNTUsMTQ3LjE5OWMwLDIuNzg3LTEuMjY3LDkuMjcxLTEzLjAzNiw5LjI3MWgtNTQuMDM3djE3OC44NTZjMC4wNzIsMC40OCwwLjE0NCwxLjE1OSwwLjE0NCwxLjkzOSAgICAgIGMwLDMuMTc3LTEuMjA3LDYuMTA2LTMuNDE2LDguMjY5Yy0yLjg1OCwyLjc5OC03LjIyNCw0LjIyMi0xMi45ODgsNC4yMjJoLTgzLjA1NmMtMTEuNDkzLDAtMTQuNTI1LTguMTQ5LTE0LjUyNS0xMi40NTRWMTYwLjIzNiAgICAgIEg2Ny42MDZjLTEzLjg0MSwwLTE1LjkwNC02LjU5NC0xNS45MDQtMTAuNTIxYzAtNi4yOTMsNS45OTYtMTIuNTc3LDcuMTk3LTEzLjc3NWMzLjE3Ni00LjMwNSw4OS4wMzYtMTE4LjE5NSwxMDEuNTI5LTEzMC43MTggICAgICBjNC41NTgtNC41MzQsOS4xMzEtNS4zMzksMTIuMTYzLTUuMjA5YzcuMjkzLDAuMywxMi4yNjgsNS45MTUsMTIuODA4LDYuNTZsMTA0LjgzOCwxMjYuNjc0ICAgICAgQzI5MS43NSwxMzQuNjMxLDI5OC4wNTUsMTQxLjA2OCwyOTguMDU1LDE0Ny4xOTl6IiBmaWxsPSIjMDAwMDAwIi8+CgkJCTwvZz4KCQk8L2c+Cgk8L2c+CjwvZz4KPGc+CjwvZz4KPGc+CjwvZz4KPGc+CjwvZz4KPGc+CjwvZz4KPGc+CjwvZz4KPGc+CjwvZz4KPGc+CjwvZz4KPGc+CjwvZz4KPGc+CjwvZz4KPGc+CjwvZz4KPGc+CjwvZz4KPGc+CjwvZz4KPGc+CjwvZz4KPGc+CjwvZz4KPGc+CjwvZz4KPC9zdmc+Cg==',
        turnRight: 'data:image/svg+xml;utf8;base64,PD94bWwgdmVyc2lvbj0iMS4wIiBlbmNvZGluZz0iaXNvLTg4NTktMSI/Pgo8IS0tIEdlbmVyYXRvcjogQWRvYmUgSWxsdXN0cmF0b3IgMTguMC4wLCBTVkcgRXhwb3J0IFBsdWctSW4gLiBTVkcgVmVyc2lvbjogNi4wMCBCdWlsZCAwKSAgLS0+CjwhRE9DVFlQRSBzdmcgUFVCTElDICItLy9XM0MvL0RURCBTVkcgMS4xLy9FTiIgImh0dHA6Ly93d3cudzMub3JnL0dyYXBoaWNzL1NWRy8xLjEvRFREL3N2ZzExLmR0ZCI+CjxzdmcgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIiB4bWxuczp4bGluaz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94bGluayIgdmVyc2lvbj0iMS4xIiBpZD0iQ2FwYV8xIiB4PSIwcHgiIHk9IjBweCIgdmlld0JveD0iMCAwIDQ5Ny40NTUgNDk3LjQ1NSIgc3R5bGU9ImVuYWJsZS1iYWNrZ3JvdW5kOm5ldyAwIDAgNDk3LjQ1NSA0OTcuNDU1OyIgeG1sOnNwYWNlPSJwcmVzZXJ2ZSIgd2lkdGg9IjMycHgiIGhlaWdodD0iMzJweCI+CjxwYXRoIGlkPSJYTUxJRF8yNV8iIGQ9Ik00MzguMzI1LDkwLjY0MUwyNTYuMDQ0LDAuNTQzYy0xLjYyNi0wLjgwNS0zLjU2NC0wLjcxLTUuMTAzLDAuMjQ5Yy0xLjUzOSwwLjk2MS0yLjQ4MiwyLjY0Ny0yLjQ4Miw0LjQ2NSAgdjM2Ljk1N2gtOC4zMDRjLTEwMS40MjcsMC0xODMuOTQ5LDgyLjUyMS0xODMuOTQ5LDE4My45NTF2MjcxLjI5aDEwNi4yODF2LTI3MS4yOWMwLTQyLjgzMSwzNC44MzgtNzcuNjcsNzcuNjY4LTc3LjY3aDguMzA0djM2Ljk1NyAgYzAsMS44MTcsMC45NDMsMy41MDQsMi40ODIsNC40NjRjMS41MzksMC45NiwzLjQ3NywxLjA1Niw1LjEwMywwLjI1MmwxODIuMjgyLTkwLjFjMS43OTEtMC44OTIsMi45MjQtMi43MTYsMi45MjQtNC43MTQgIFM0NDAuMTE2LDkxLjUzMiw0MzguMzI1LDkwLjY0MXoiIGZpbGw9IiMwMDAwMDAiLz4KPGc+CjwvZz4KPGc+CjwvZz4KPGc+CjwvZz4KPGc+CjwvZz4KPGc+CjwvZz4KPGc+CjwvZz4KPGc+CjwvZz4KPGc+CjwvZz4KPGc+CjwvZz4KPGc+CjwvZz4KPGc+CjwvZz4KPGc+CjwvZz4KPGc+CjwvZz4KPGc+CjwvZz4KPGc+CjwvZz4KPC9zdmc+Cg=='
      }
    }
  },
  methods: {
    getColorItem (item) {
      return item.color != null ? item.color : 'grey'
    },
    getSign (item) {
      return this.signSources[item.sign]
    },
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
  }
}
</script>

<style scoped>
.item {
  width: 30px;
  height: 30px;
  float: left;
  border: 5px solid white;
}
</style>
