<template>
  <div id="app">
    <div id="min_div">
      <tian-min/>
      <!-- <tian-min-tencent/> -->
      <!-- <life-and-death/> -->
      <!-- <life-death/>
      <life-and-death-tencent/> -->
    </div>
  </div>
</template>

<script>
// import * as d3 from 'd3'
import TianMin from "./components/TianMin";
// import TianMinTencent from "./components/TianMinTencent";
// import LifeAndDeath from "./components/LifeAndDeath";
// import LifeDeath from "./components/LifeDeath";
// import LifeAndDeathTencent from "./components/LifeAndDeathTencent"
export default {
  name: "app",
  components: {
    TianMin,
    // TianMinTencent,
    // LifeAndDeath,
    // LifeDeath,
    // LifeAndDeathTencent
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
  position: absolute;
  left: 0;
  right: 0;
  top: 0;
  // width: 100%;
  // height: 100%;
  // color: #2c3e50;
  // margin-top: 60px;
}

#min_div {
  // position: absolute;
  left: 0;
  right: 0;
  // width: 100%;
  // height: 100%;
  // border: 1px solid red;
  text-align: center;
  // height: 100%;
  overflow: hidden;
}
</style>
