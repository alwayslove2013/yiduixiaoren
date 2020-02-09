<template>
  <div id="cure_rate_div">
    <div id="title">
      <p class="title_0">各地区患者病亡率与治愈率</p>
      <p class="title_1">截止{{date}} {{time}} 数据统计</p>
    </div>

    <div id="explanation">
      <p class="title">图表解读</p>
      <div id="explanation_text">病亡率为该地区公布的死亡人数在确诊人数中的占比；治愈率为该地区治愈人数在确诊人数中的占比。</div>
    </div>

    <div id="distribution">
      <p class="title">每日比率态势</p>
      <div id="barChart"></div>
    </div>

    <div id="time_select">
      <p class="title">选择日期查看各地区比率</p>
      <div id="legend">
        
      </div>
      <div id="control_panel">
        <div id="scroll_x_panel" :style="`width: ${90 * date_select_set.length + 1}px;`">
          <div
            v-for="(date, index) in date_select_set"
            :class="`date_select_div ${date_select===index?'selected':''}`"
            @click="date_select = index"
            :key="'date' + index"
          >{{date}}</div>
        </div>
      </div>
      <div id="block_div">
        <div v-for="block in blockData"
          class="block_svg_div"
          :key="block.title">
          <svg
            :style="block_color(block)"
            :width="block_length"
            :height="block_length">
            <path
              class="cure"
              :d="cure_rect_d(block)"/>
            <path
              class="death"
              :d="death_rect_d(block)"/>
          </svg>
          <p>{{block.title}}</p>
        </div>
      </div>
    </div>

    <div id="percent_div">
      <div id="legend">
        <img class="people_icon" src="../assets/people_cure.svg" />
        <span>治愈人数</span>
        <img class="people_icon" src="../assets/people_death.svg" />
        <span>病亡人数</span>
        <img class="people_icon" src="../assets/people_diagnosis.svg" />
        <span>确诊人数</span>
      </div>

      <div v-for="area in dataset" :key="area.title_1" class="area_precent_div">
        <div class="head">
          <span class="title_1">{{area.title_1}}</span>
          <span class="title_2">{{area.title_2}}</span>
          <span class="num diagnosis">{{area.quezhen}}</span>
          <span class="num death">{{area.siwang}}</span>
          <span class="num cure">{{area.zhiyu}}</span>
        </div>
        <div class="area_svg_div">
          <svg width="100%" height="100%" class="area_svg">
            <defs>
              <clipPath v-for="index in clips" :key="'left' + index" :id="'left-cut-' + index">
                <rect x="0" y="0" :width="10 * (index+0.5)/10 + 'px'" height="1000px" />
              </clipPath>
              <clipPath v-for="index in clips" :key="'right' + index" :id="'right-cut-' + index">
                <rect :x="10 * (9.5 - index)/10 + 'px'" y="0" width="1000px" height="1000px" />
              </clipPath>
            </defs>
            <!-- <path class="cure"
            :d="icon_path_d"/>-->
            <g id="icon_people">
              <path
                v-for="icon in icons"
                :key="icon"
                :d="icon_path_d"
                :style="icon_position(icon)"
                :class="icon_class(area, icon)"
              />
            </g>
            <path
              id="cure_clip"
              :d="icon_path_d"
              class="cure"
              :clip-path="cure_clip_path(area)"
              :style="cure_clip_position(area)"
            />
            <path
              id="death_clip"
              :d="icon_path_d"
              class="death"
              :clip-path="death_clip_path(area)"
              :style="death_clip_position(area)"
            />
            <g id="rate">
              <!-- <g class="background">
                <text
                  class="cure_rate"
                >{{(Math.round(area.zhiyu / area.quezhen * 10000) / 100).toFixed(2)}}%</text>
                <text
                  class="death_rate"
                >{{(Math.round(area.siwang / area.quezhen * 10000) / 100).toFixed(2)}}%</text>
              </g>-->
              <g class="front">
                <text
                  class="cure_rate cure"
                >{{(Math.round(area.zhiyu / area.quezhen * 10000) / 100).toFixed(2)}}%</text>
                <text
                  class="death_rate death"
                >{{(Math.round(area.siwang / area.quezhen * 10000) / 100).toFixed(2)}}%</text>
              </g>
            </g>
          </svg>
        </div>
      </div>
    </div>

    <div id="footer">
      <img src="../assets/占比logo.svg" width="100%" />
    </div>
  </div>
</template>

<script>
import * as d3 from "d3";
export default {
  name: "cure_rate",
  data() {
    return {
      date: "2020-02-06",
      time: "18:12:34",
      icons: [],
      clips: [],
      svgWidth: 0,
      svgHeight: 0,
      iconStepX: 0,
      iconStepY: 0,
      iconScale: 0,
      date_select: 0,
      date_select_set: [
        "2月1日",
        "2月2日",
        "2月3日",
        "2月4日",
        "2月5日",
        "2月6日",
        "2月7日",
        "2月8日"
      ],
      blockData: [
        {
          title: '武汉',
          diagnosis: 8351,
          cure: 368,
          death: 362,
        },
        {
          title: "湖北",
          death: 117,
          cure: 152,
          diagnosis: 8327
        },
        {
          title: "全国",
          death: 13,
          cure: 401,
          diagnosis: 7699
        },
        {
          title: "海外",
          death: 1,
          cure: 19,
          diagnosis: 193
        }
      ],
      dataset: [
        {
          title_1: "武汉",
          title_2: "",
          siwang: 362,
          zhiyu: 368,
          quezhen: 8351
        },
        {
          title_1: "湖北",
          title_2: "（除武汉）",
          siwang: 117,
          zhiyu: 152,
          quezhen: 8327
        },
        {
          title_1: "全国",
          title_2: "（除湖北、包括港澳台地区）",
          siwang: 13,
          zhiyu: 401,
          quezhen: 7699
        },
        {
          title_1: "海外",
          title_2: "",
          siwang: 1,
          zhiyu: 19,
          quezhen: 193
        }
      ],
      icon_path_d:
        "M10,6.87269213 L10,11.1273079 C10,11.4000644 9.90887885,11.6318724 9.72646878,11.8227317 C9.5442265,12.0137667 9.32288434,12.1090206 9.06244233,12.1090206 C8.80200031,12.1090206 8.58065817,12.013591 8.39841587,11.8227317 C8.21600578,11.6316966 8.12488463,11.4000644 8.12488463,11.1273079 L8.12488463,7.52734303 L7.49979025,7.52734303 L7.49979025,16.8546685 C7.49979025,17.1683737 7.39239148,17.4376153 7.17759393,17.6625692 C6.96262859,17.8876988 6.70554279,18 6.40616872,18 C6.10662685,18 5.84954105,17.8875231 5.63457571,17.6625692 C5.41977816,17.4376153 5.31237941,17.1681979 5.31237939,16.8546685 L5.31237939,12.1091964 L4.687285,12.1091964 L4.687285,16.8546685 C4.687285,17.1683737 4.57971842,17.4376153 4.3650887,17.6625692 C4.15012337,17.8876988 3.89303756,18 3.59366348,18 C3.29412161,18 3.0370358,17.8875231 2.82207046,17.6625692 C2.60727292,17.4376153 2.49987416,17.1681979 2.49987415,16.8546685 L2.49987415,7.52734303 L1.87494757,7.52734303 L1.87494757,11.1273079 C1.87494757,11.4000644 1.78382642,11.6318724 1.60158414,11.8227317 C1.41917405,12.0137667 1.19799971,12.1090206 0.937557691,12.1090206 C0.677115675,12.1090206 0.455773536,12.013591 0.273531239,11.8227317 C0.0911211483,11.6316966 0,11.4000644 0,11.1273079 L0,6.87269213 C0,6.32735474 0.182410091,5.86356314 0.546894667,5.48166879 C0.911547055,5.09977445 1.35423135,4.90891516 1.87494757,4.90891516 L8.12505245,4.90891516 C8.64576867,4.90891516 9.08862077,5.09977445 9.45327316,5.48166879 C9.81775774,5.86356314 10,6.32735474 10,6.87269213 L10,6.87269213 Z M7.18749476,2.2908388 C7.18749476,2.92492751 6.97437533,3.46534402 6.54780084,3.9119126 C6.12139417,4.35865692 5.60537665,4.58185333 4.9999161,4.58185333 C4.39445555,4.58185333 3.87843803,4.35865692 3.45203136,3.9119126 C3.02545688,3.46534402 2.81233745,2.92492751 2.81233745,2.2908388 C2.81233745,1.65675009 3.02562467,1.11650931 3.45203136,0.669764988 C3.87843803,0.223196414 4.39445555,0 4.9999161,0 C5.60537665,0 6.12122636,0.223196414 6.54780084,0.669940734 C6.97420751,1.11650931 7.18749476,1.65692582 7.18749476,2.2908388 Z"
    };
  },
  computed: {
    block_length() {
      return this.svgWidth * 0.22
    }
  },
  methods: {
    icon_position(index) {
      let x = index % 20;
      let y = parseInt(index / 20);
      let translate = `translate(${x * this.iconStepX}px, ${y *
        this.iconStepY}px)`;
      let scale = `scale(${this.iconScale})`;
      return `transform: ${translate} ${scale};`;
    },
    icon_class(area, index) {
      if ((index + 1) / 100 < area.zhiyu / area.quezhen) {
        return "cure";
      }
      if ((100 - index) / 100 < area.siwang / area.quezhen) {
        return "death";
      }
      return "diagnosis";
    },
    cure_clip_path(area) {
      let num = parseInt((area.zhiyu / area.quezhen) * 1000) % 10;
      return `url(#left-cut-${num})`;
    },
    cure_clip_position(area) {
      let index = parseInt((area.zhiyu / area.quezhen) * 100);
      let x = index % 20;
      let y = parseInt(index / 20);
      let translate = `translate(${x * this.iconStepX}px, ${y *
        this.iconStepY}px)`;
      let scale = `scale(${this.iconScale})`;
      return `transform: ${translate} ${scale}`;
    },
    death_clip_path(area) {
      let num = parseInt((area.siwang / area.quezhen) * 1000) % 10;
      return `url(#right-cut-${num})`;
    },
    death_clip_position(area) {
      let index = 99 - parseInt((area.siwang / area.quezhen) * 100);
      let x = index % 20;
      let y = parseInt(index / 20);
      let translate = `translate(${x * this.iconStepX}px, ${y *
        this.iconStepY}px)`;
      let scale = `scale(${this.iconScale})`;
      return `transform: ${translate} ${scale}`;
    },
    block_color(block) {
      let color_v_max = 8000;
      let color = d3.interpolateRgb('#F6DBDB', '#DA6B6B')
      console.log(color(0), color(0.5), color(1))
      let color_v = block.diagnosis > color_v_max ? 1 : block.diagnosis / color_v_max
      console.log()
      return `background: ${color(color_v)};`
    },
    cure_rect_d(block) {
      let svgWidth = this.svgWidth * 0.22
      let rectWidth = Math.sqrt((block.cure + block.death) / block.diagnosis * svgWidth * svgWidth)
      let x = (svgWidth - rectWidth) / 2
      let dy =  block.cure / (block.cure + block.death) * rectWidth
      return `M${x},${x}l${rectWidth},0l0,${dy}l${-rectWidth},0Z`
    },
    death_rect_d(block) {
      let svgWidth = this.svgWidth * 0.22
      let rectWidth = Math.sqrt((block.cure + block.death) / block.diagnosis * svgWidth * svgWidth)
      let x = (svgWidth - rectWidth) / 2
      let dy =  block.death / (block.cure + block.death) * rectWidth
      return `M${x},${svgWidth-x}l${rectWidth},0l0,${-dy}l${-rectWidth},0Z`
    }
  },
  mounted: async function() {
    function generate_range(n) {
      let a = Array(n).fill(0);
      let tmp = a.map((d, i) => i);
      // console.log('tmp', tmp, a)
      return tmp;
    }
    this.icons = generate_range(100);
    this.clips = generate_range(10);
    let svgRect = d3
      .select(".area_svg_div")
      .node()
      .getBoundingClientRect();
    this.svgWidth = svgRect.width;
    this.svgHeight = svgRect.height;
    this.iconStepX = (this.svgWidth * 16) / (10 * 20 + 6 * 19);
    this.iconStepY = (this.svgHeight * 22) / (18 * 5 + 4 * 4);
    this.iconScale = this.iconStepX / 16;
    console.log(
      this.svgWidth,
      this.svgHeight,
      this.iconStepX,
      this.iconStepY,
      this.iconScale
    );
  }
};
</script>

<style lang="less">
@font-face {
  font-family: "Khand-SemiBold";
  src: url("../assets/font/khand/Khand-SemiBold.ttf");
}

@font-face {
  font-family: "Khand-Bold";
  src: url("../assets/font/khand/Khand-Bold.ttf");
}

@font-face {
  font-family: "Khand-Regular";
  src: url("../assets/font/khand/Khand-Regular.ttf");
}
@border-left: 48px;
#cure_rate_div {
  position: absolute;
  left: @border-left;
  right: @border-left;
  // width: 80%;
  // margin: auto;
  // border: 1px solid red;
  text-align: left;
  line-height: 0;
  // overflow: hidden;
}

#title {
  // position: relative;
  margin-top: 50px;
  width: 100%;
  height: 100%;
  .title_0 {
    font-size: 20px;
    font-weight: bold;
    color: #000000;
  }
  .title_1 {
    font-size: 12px;
    color: #4e4e4e;
  }
}

.title {
  font-size: 18px;
  font-weight: bold;
  color: #4a4a4a;
}

#explanation {
  // position: relative;
  margin-top: 30px;
  height: 100%;
  // border: 1px solid red;
  #explanation_text {
    position: relative;
    top: 0px;
    line-height: 12px;
    font-size: 12px;
    // border: 1px solid green;
    padding: 20px 16px 25px 16px;
    background: #f7f7f7;
    box-shadow: 1px 1px 1px rgba(0, 0, 0, 0.2);
  }
}

#distribution {
  margin-top: 30px;
  #barChart {
    width: 100%;
    height: 200px;
    background: rgb(236, 236, 236);
  }
}

#time_select {
  // position: relative;
  margin-top: 50px;
  height: 100%;
  // border: 1px solid blue;
  #legend {
    margin-top: 20px;
    width: 100%;
    height: 100px;
    background: rgba(236, 236, 236, 0.3);
  }
  #control_panel {
    // position: relative;
    margin-top: 20px;
    width: 100%;
    height: 30px;
    overflow: scroll;
    &::-webkit-scrollbar {display:none}
    // background: rgb(236, 236, 236);
    #scroll_x_panel {
      height: 100%;
      margin-top: 2px;
      line-height: 20px;
      // background: rgb(236, 236, 236);
      .date_select_div {
        float: left;
        width: 80px;
        margin: 0 5px 0 5px;
        font-size: 10px;
        height: 25px;
        line-height: 25px;
        text-align: center;
        vertical-align: middle;
        // border: 1px solid red;
        border-radius: 15px;
        box-shadow: 1px 1px 5px rgba(0, 0, 0, 0.1);
        cursor: pointer;
      }
      .selected {
        background: #4A90E2;
        color: white;
      }
    }
  }
  #block_div {
    margin-top: 25px;
    width: 100%;
    height: 25vw;
    .block_svg_div {
      float: left;
      width: 22%;
      height: 100%;
      // background: green;
      margin-right: 4%;
      font-size: 13;
      font-weight: 500;
      color: #4a4a4a;
      text-align: center;
      &:last-child {
        margin-right: 0;
      }
    }
  }
}

.people_icon {
  width: 16px;
  transform: translate(0, 9px);
  font-size: 12px;
  color: #4a4a4a;
  margin-right: 8px;
  span + & {
    margin-left: 20px;
  }
}

.cure {
  fill: #18babd;
  color: #18babd;
}

.death {
  fill: #6f6f6f;
  color: #6f6f6f;
}

.diagnosis {
  fill: #d75e5e;
  color: #d75e5e;
}

#percent_div {
  margin-top: 20px;
  width: 100%;
  height: 100%;
  line-height: 16px;
  #legend {
    font-size: 12px;
    color: #4a4a4a;
    margin-bottom: 40px;
  }
  .area_precent_div {
    height: 100%;
    // border: 1px solid red;
    margin-bottom: 50px;
    &:last-child {
      margin-bottom: 50px;
    }
    .head {
      width: 100%;
      padding-bottom: 4px;
      border-bottom: 1px solid #979797;
      .title_1 {
        font-size: 14px;
        font-weight: bold;
      }
      .title_2 {
        font-size: 12px;
      }
      .num {
        float: right;
        font-family: "Khand-SemiBold";
        font-size: 20px;
        padding-left: 5px;
        padding-right: 5px;
        border-right: 1px solid #979797;
        padding-top: 2px;
        &:nth-child(3) {
          padding-right: 0;
          border-right: none;
        }
        // line-height: 14px;
      }
    }
    @scale_: 0.4;
    .area_svg_div {
      margin-top: 10px;
      // background:rgba(0, 0, 0, 0.2);
      width: 100%;
      // width: calc(~"100vw - @{border-left} * 2");
      height: calc(~"(100vw - @{border-left} * 2) * @{scale_}");
      .area_svg {
        #rate {
          transform: translate(0, 65%);
          transform-origin: center;
          font-family: "Khand-Bold";
          .cure_rate {
            transform: translate(8%, 0);
            text-anchor: center;
          }
          .death_rate {
            transform: translate(54%, 0);
          }
          .background {
            font-size: 12vw;
            // font-size: 13vw;
            // transform: translate(-1.5vw, 0.5vw);
            fill: white;
          }
          .front {
            font-size: 14vw;
            stroke-width: 0.5vw;
            // stroke: rgb(236, 236, 236);
            stroke: white;
          }
        }
      }
    }
  }
}
</style>