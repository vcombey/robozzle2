<template>
  <div>
    <stack :stack="stack"></stack>
    <br />
    <br />
    <br />
    <br />

    <div class="col-xs-12 col-md-8">
    {{ pos.x }} {{ pos.y }}
      <div v-for="(lines, l) in grid">
        <div v-for="(elem, c) in lines">
          <div class="item" :style="{ backgroundColor: getColor(elem) }">
            <player v-if="l == pos.l && c == pos.c" :dir="dir" src='data:image/svg+xml;utf8;base64,PD94bWwgdmVyc2lvbj0iMS4wIiBlbmNvZGluZz0iaXNvLTg4NTktMSI/Pgo8IS0tIEdlbmVyYXRvcjogQWRvYmUgSWxsdXN0cmF0b3IgMTguMS4xLCBTVkcgRXhwb3J0IFBsdWctSW4gLiBTVkcgVmVyc2lvbjogNi4wMCBCdWlsZCAwKSAgLS0+CjxzdmcgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIiB4bWxuczp4bGluaz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94bGluayIgdmVyc2lvbj0iMS4xIiBpZD0iQ2FwYV8xIiB4PSIwcHgiIHk9IjBweCIgdmlld0JveD0iMCAwIDIyLjA2MiAyMi4wNjIiIHN0eWxlPSJlbmFibGUtYmFja2dyb3VuZDpuZXcgMCAwIDIyLjA2MiAyMi4wNjI7IiB4bWw6c3BhY2U9InByZXNlcnZlIiB3aWR0aD0iMzJweCIgaGVpZ2h0PSIzMnB4Ij4KPGc+Cgk8cGF0aCBkPSJNMTAuNTQ0LDExLjAzMWw2Ljc0Mi02Ljc0MmMwLjgxLTAuODA5LDAuODEtMi4xMzUsMC0yLjk0NGwtMC43MzctMC43MzcgICBjLTAuODEtMC44MTEtMi4xMzUtMC44MTEtMi45NDUsMEw0Ljc2OSw5LjQ0M2MtMC40MzUsMC40MzQtMC42MjgsMS4wMTctMC41OTcsMS41ODljLTAuMDMxLDAuNTcxLDAuMTYyLDEuMTU0LDAuNTk3LDEuNTg4ICAgbDguODM1LDguODM0YzAuODEsMC44MTEsMi4xMzUsMC44MTEsMi45NDUsMGwwLjczNy0wLjczN2MwLjgxLTAuODA4LDAuODEtMi4xMzQsMC0yLjk0M0wxMC41NDQsMTEuMDMxeiIgZmlsbD0iIzAwMDAwMCIvPgo8L2c+CjxnPgo8L2c+CjxnPgo8L2c+CjxnPgo8L2c+CjxnPgo8L2c+CjxnPgo8L2c+CjxnPgo8L2c+CjxnPgo8L2c+CjxnPgo8L2c+CjxnPgo8L2c+CjxnPgo8L2c+CjxnPgo8L2c+CjxnPgo8L2c+CjxnPgo8L2c+CjxnPgo8L2c+CjxnPgo8L2c+Cjwvc3ZnPgo='>
          </player>
          </div>
            </div>
            <br />
        <br />
      </div>
    <button @click.prevent="executeCode"> start </button>
    <button @click.prevent="pause"> pause </button>
    <button @click.prevent="reset"> reset </button>
    <button @click.prevent="executeItem(stack.shift())"> move </button>
  </div>
</div>
</template>

<script>
  import player from './player.vue'
  import stack from './stack.vue'
  export default {
    props: ['code'],
    data () {
      return {
        intervalId: 0,
        grid: [
          [null, null, 'grey', 'blue'],
          [null, 'blue', 'grey', null],
          ['blue', 'blue', null, null],
          ['blue', null, null, null]
        ],
        stack: this.code.f1.slice(0),
        pos: {l: 3, c: 0},
        initialPos: {l: 3, c: 0},
        initialDir: 0,
        dir: 0
      }
    },
    methods: {
      getColor (elem) {
        return elem != null ? elem : 'white'
      },
      move () {
        if (this.dir === 0) { // up
          this.pos.l--
        } else if (this.dir === 1) { // right
          this.pos.c++
        } else if (this.dir === 2) { // down
          this.pos.l++
        } else if (this.dir === 3) { // left
          this.pos.c--
        }
        if (this.grid[this.pos.l][this.pos.c] === null) {
          alert('game over')
        }
      },
      executeItem (elem) {
        console.log(this.initialPos)
        console.log(this.grid[this.pos.l][this.pos.c])
        if (elem.color === this.grid[this.pos.l][this.pos.c] || elem.color === 'grey' || this.grid[this.pos.l][this.pos.c] === null) {
          if (elem.sign === 'straight') {
            console.log('straight')
            this.move()
          } else if (elem.sign === 'turnRight') {
            this.dir = (this.dir + 1) % 4
          } else if (elem.sign === 'turnLeft') {
            this.dir = this.dir === 0 ? 3 : this.dir - 1
          } else if (elem.sign === 'f1') {
            this.stack = this.code.f1.slice(0).concat(this.stack)
          }
        }
      },
      executeCode () {
        this.intervalId = setInterval(() => {
          if (this.stack.length === 0) {
            clearInterval(this.intervalId)
          } else {
            this.executeItem(this.stack.shift())
          }
        }, 300)
      },
      pause () {
        if (this.intervalId) {
          clearInterval(this.intervalId)
          this.intervalId = 0
        }
      },
      reset () {
        if (this.intervalId) {
          clearInterval(this.intervalId)
          this.intervalId = 0
        }
        this.stack = this.code.f1.slice(0)
        this.pos.c = this.initialPos.c
        this.pos.l = this.initialPos.l
        this.dir = this.initialDir
      }
    },
    components: {
      'stack': stack,
      'player': player
    }
  }
</script>

<style scoped>
  .item {
    width: 35px;
    height: 35px;
    float: left;
    background-color: grey;
    border: 1px solid white;
  }
</style>
