<template>
  <div id="app">
    <b-navbar class="nav" toggleable type="inverse" variant="success">

      <b-nav-toggle target="nav_collapse"></b-nav-toggle>

      <b-link class="navbar-brand" to="#">
        <span>Robozzle-2</span>
      </b-link>

      <b-collapse is-nav id="nav_collapse">

        <b-nav is-nav-bar>
          <b-nav-item>all levels</b-nav-item>
          <b-nav-item>Create level</b-nav-item>
          <b-nav-item>Contact</b-nav-item>
        </b-nav>

        <b-nav is-nav-bar class="ml-auto">


          <b-nav-item-dropdown right>

            <!-- Using button-content slot -->
            <template slot="button-content">
              <span style="font-weight: bold;">User</span>
            </template>

            <b-dropdown-item to="#">Profile</b-dropdown-item>
            <b-dropdown-item to="#">Signout</b-dropdown-item>
          </b-nav-item-dropdown>

        </b-nav>
      </b-collapse>
    </b-navbar>
    <br><br><br>
<div class="container-fluid">

  <router-view></router-view>
</div>
  </div>
</template>

<script>
export default {
  name: 'app'
}
</script>

<style>
.item {
  width: 42px;
  height: 42px;
  float: left;
  background-color: #ECECEC;
  border: 1px solid #ECECEC;
}
.item-fn {
  width: 42px;
  height: 42px;
  float: left;
  background-color: #ECECEC;
  border: 1px solid white;
}
</style>
