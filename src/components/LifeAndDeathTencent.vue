<template>
  <div id="container">test</div>
</template>

<script>
// import * as d3 from 'd3'
import axios from "axios";
export default {
  name: "left-and-death-tencent",
  data() {
    return {};
  },
  methods: {
    async initData() {
      // let url = "https://ehcard-test.wecity.qq.com/api";
      // let tmp = {
      //   method: "POST",
      //   headers: { "Content-Type": "application/json" },
      //   body: {
      //     service: "THOuterDataServer",
      //     func: "getAreaInfo",
      //     args: {
      //       req: {
      //         none: ""
      //       }
      //     }
      //   }
      // };
      // let data = await fetch('/api', tmp)
      // console.log('data', data)
      axios({
        methods: "POST",
        url: "/api/abc",
        params: {},
        timeout: 10000
      }).then(res => {
        console.log("remove the tree template", res);
      });
      // d3.xhr(url)
      //   .header("Content-Type", "application/json")
      //   .post(JSON.stringify(tmp.body), function(
      //     err,
      //     rawData
      //   ) {
      //     var data = JSON.parse(rawData);
      //     console.log("got response", data);
      //   });
    }
  },
  mounted() {
    this.initData();
  }
};
</script>

<style lang="less">
@border: 30px;
#container {
  position: absolute;
  left: @border;
  right: @border;
  // background: rgba(236, 236, 236, 0.2);
  text-align: left;
}
</style>