<template>
  <div id="app">
    <div id="min_div">
      <tian-min />
    </div>
  </div>
</template>

<script>
// import * as d3 from 'd3'
import TianMin from "./components/TianMin";
export default {
  name: "app",
  components: {
    TianMin
  },
  mounted: function() {
  }
};
</script>

<style lang="less">
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  // color: #2c3e50;
  // margin-top: 60px;
}

#min_div {
  position: absolute;
  left: 0;
  right: 0;
  margin: auto;
  width: 414pt;
  height: 1052pt;
  // border: 1px solid red;
  text-align: center;
}
</style>
