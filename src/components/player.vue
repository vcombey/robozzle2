<template>
  <div :class="{ up: dir === 0, right: dir === 1, down: dir === 2, left: dir === 3 }">
  <img src='data:image/svg+xml;utf8;base64,PD94bWwgdmVyc2lvbj0iMS4wIiBlbmNvZGluZz0iaXNvLTg4NTktMSI/Pgo8IS0tIEdlbmVyYXRvcjogQWRvYmUgSWxsdXN0cmF0b3IgMTguMS4xLCBTVkcgRXhwb3J0IFBsdWctSW4gLiBTVkcgVmVyc2lvbjogNi4wMCBCdWlsZCAwKSAgLS0+CjxzdmcgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIiB4bWxuczp4bGluaz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94bGluayIgdmVyc2lvbj0iMS4xIiBpZD0iQ2FwYV8xIiB4PSIwcHgiIHk9IjBweCIgdmlld0JveD0iMCAwIDIyLjA2MiAyMi4wNjIiIHN0eWxlPSJlbmFibGUtYmFja2dyb3VuZDpuZXcgMCAwIDIyLjA2MiAyMi4wNjI7IiB4bWw6c3BhY2U9InByZXNlcnZlIiB3aWR0aD0iMzJweCIgaGVpZ2h0PSIzMnB4Ij4KPGc+Cgk8cGF0aCBkPSJNMTAuNTQ0LDExLjAzMWw2Ljc0Mi02Ljc0MmMwLjgxLTAuODA5LDAuODEtMi4xMzUsMC0yLjk0NGwtMC43MzctMC43MzcgICBjLTAuODEtMC44MTEtMi4xMzUtMC44MTEtMi45NDUsMEw0Ljc2OSw5LjQ0M2MtMC40MzUsMC40MzQtMC42MjgsMS4wMTctMC41OTcsMS41ODljLTAuMDMxLDAuNTcxLDAuMTYyLDEuMTU0LDAuNTk3LDEuNTg4ICAgbDguODM1LDguODM0YzAuODEsMC44MTEsMi4xMzUsMC44MTEsMi45NDUsMGwwLjczNy0wLjczN2MwLjgxLTAuODA4LDAuODEtMi4xMzQsMC0yLjk0M0wxMC41NDQsMTEuMDMxeiIgZmlsbD0iIzAwMDAwMCIvPgo8L2c+CjxnPgo8L2c+CjxnPgo8L2c+CjxnPgo8L2c+CjxnPgo8L2c+CjxnPgo8L2c+CjxnPgo8L2c+CjxnPgo8L2c+CjxnPgo8L2c+CjxnPgo8L2c+CjxnPgo8L2c+CjxnPgo8L2c+CjxnPgo8L2c+CjxnPgo8L2c+CjxnPgo8L2c+CjxnPgo8L2c+Cjwvc3ZnPgo=' >
  </div>
</template>

<script>
  export default {
    props: ['src', 'dir'],
    methods: {
      getDirection () {
        if (this.dir === 0) {
          return 'up'
        } else if (this.dir === 2) {
          return 'right'
        } else if (this.dir === 3) {
          return 'down'
        } else if (this.dir === 4) {
          return 'left'
        }
      }
    }
  }
</script>

<style scoped>
.up {
    -ms-transform: rotate(90deg); /* IE 9 */
    -webkit-transform: rotate(90deg); /* Chrome, Safari, Opera */
    transform: rotate(90deg);
  }
.down {
  -ms-transform: rotate(-90deg); /* IE 9 */
  -webkit-transform: rotate(-90deg); /* Chrome, Safari, Opera */
  transform: rotate(-90deg);
}
.left {
   -ms-transform: rotate(0deg); /* IE 9 */
   -webkit-transform: rotate(0deg); /* Chrome, Safari, Opera */
   transform: rotate(0deg);
}
.right {
  -ms-transform: rotate(180deg); /* IE 9 */
  -webkit-transform: rotate(180deg); /* Chrome, Safari, Opera */
  transform: rotate(180deg);
}
</style>
