<template>
  <div id="app">
    <div id="min_div">
      <tian-min/>
    </div>
  </div>
</template>

<script>
import TianMin from "./components/TianMin"
export default {
  name: 'app',
  components: {
    TianMin
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

#min_div {
  position: absolute;
  width: 800px;
  border: 1px solid red;
}
</style>
