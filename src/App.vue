<template>
  <div id="app">
    <router-view></router-view>
  </div>
</template>

<script>
export default {
    name: 'app'
}
</script>

<style>
  #app {

  }
  * {
    margin: 0;
    padding: 0;
  }
  html, body, #app, .wrapper {
    width: 100%;
    height: 100%;
    background-color: deepskyblue;
  }
  body {
    font-family: "microsoft yahei","PingFang-SC-Regular","Helvetica Neue", Helvetica, arial, STHeiTi, sans-serif;
  }
  a {
    text-decoration: none
  }
</style>
