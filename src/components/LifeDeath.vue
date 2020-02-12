<template>
  <div id="container">
    <div id="head">
      <div id="left_border" />
      <div id="title">新冠肺炎疫情生死线</div>
      <div id="description">(7:00-10:00为更新高峰，数据有滞后请谅解)</div>
    </div>

    <div id="explanation">
      <div id="explanation_text">病亡率为该地区公布的死亡人数在确诊人数中的占比；治愈率为该地区治愈人数在确诊人数中的占比。</div>
    </div>

    <div id="total">
      <div class="title">累计治愈和病亡病例（{{select_time}}）</div>
      <div id="legend">
        <div class="legend_part">
          <div class="diagnosis icon" />
          <div class="legend_text">确诊人数</div>
        </div>
        <div class="legend_part">
          <div class="cure icon" />
          <div class="legend_text">治愈人数</div>
        </div>
        <div class="legend_part">
          <div class="death icon" />
          <div class="legend_text">病亡人数</div>
        </div>
      </div>
      <div id="total_svg_div">
        <svg id="total_svg" width="100%" height="100%">
          <g class="label_line">
            <path
              v-for="(line, index) in total_x_label"
              :key="line + `${index}`"
              class="total_label_line"
              :d="index===(total_x_label.length - 1) ? `M${total_begin_x + (index+0.5)*total_step_x},5v${total_svg_height-25}` : `M${total_begin_x + index*total_step_x},5v${total_svg_height-25}`"
            />
          </g>
          <g
            :style="`transform: translate(${total_begin_x}px, ${total_svg_height}px);`"
            class="x_label"
          >
            <text
              v-for="(label, index) in total_x_label"
              class="label_text"
              :style="`transform: translate(${index===(total_x_label.length - 1) ? total_step_x * (index + 0.5) : total_step_x * index}px, -5px)`"
              :key="label + `${index}`"
            >{{num2text(label)}}</text>
            <text
              class="label_text"
              :style="`transform: translate(${total_step_x * (total_x_label.length - 2.5)}px, -5px);`"
            >//</text>
          </g>
          <g
            v-for="(data, index) in total_dataset"
            :key="data.title_1"
            :style="total_svg_g_style(index)"
          >
            <text style="transform: translate(0, 20px)">
              <tspan x="10" font-size="16" font-weight="bold">{{data.title_1}}</tspan>
              <tspan x="-5" dy="16" font-size="14" fill="#888888">{{data.title_2}}</tspan>
            </text>
            <rect
              :x="total_begin_x"
              y="5"
              :width="total_bar_width(data.quezhen)"
              height="12"
              class="diagnosis"
            />
            <text class="bar_text" y="15" :x="total_begin_x + 1">{{num2text(data.quezhen)}}</text>
            <rect
              :x="total_begin_x"
              y="17"
              :width="total_bar_width(data.zhiyu)"
              height="12"
              class="cure"
            />
            <text class="bar_text" y="27" :x="total_begin_x + 1">{{num2text(data.zhiyu)}}</text>
            <rect
              :x="total_begin_x + total_bar_width(data.zhiyu)"
              y="17"
              :width="total_bar_width(data.siwang)"
              height="12"
              class="death"
            />
            <text
              class="bar_text"
              y="27"
              :style="data.siwang < 100 ? `text-anchor: end; transform: translate(${total_bar_width(data.siwang) - 3}px, 0)` : ''"
              :x="total_begin_x + total_bar_width(data.zhiyu) + 1"
            >{{num2text(data.siwang)}}</text>
            <g
              id="页面1"
              stroke="none"
              stroke-width="1"
              fill="none"
              :style="`transform: translate(${total_begin_x + total_step_x * (total_x_label.length - 2.8)}px, 0) scale(0.5)`"
              fill-rule="evenodd"
            >
              <g id="手机" transform="translate(-528.000000, -748.000000)" fill="#FFFFFF">
                <g id="编组-35" transform="translate(34.000000, 71.000000)">
                  <g id="编组-36" transform="translate(0.000000, 585.000000)">
                    <g id="编组-26" transform="translate(490.000000, 86.000000)">
                      <g id="编组-25" transform="translate(0.490312, 0.597389)">
                        <g
                          id="编组-24"
                          transform="translate(28.424015, 26.671522) rotate(23.000000) translate(-28.424015, -26.671522) translate(13.924015, 4.171522)"
                        >
                          <g id="编组-22">
                            <g id="编组-21">
                              <g id="编组-20">
                                <polygon
                                  id="路径-11"
                                  points="13.9266941 1.26121336e-13 1.11910481e-13 8.64947511 14.1532193 16.1404361 28.3064386 8.64947511"
                                />
                                <polygon
                                  id="路径-11"
                                  points="13.9266941 7.05592105 -1.17239551e-13 15.7053962 14.1532193 23.1963572 28.3064386 15.7053962"
                                />
                                <polygon
                                  id="路径-11"
                                  points="13.9266941 21.1677632 -1.17239551e-13 29.8172383 14.1532193 37.3081993 28.3064386 29.8172383"
                                />
                              </g>
                              <polygon
                                id="路径-11"
                                points="13.9266941 14.1118421 -1.17239551e-13 22.7613172 14.1532193 30.2522782 28.3064386 22.7613172"
                              />
                            </g>
                            <polygon
                              id="路径-11"
                              points="13.9266941 28.2236842 1.10134124e-13 36.8731593 14.1532193 44.3641203 28.3064386 36.8731593"
                            />
                          </g>
                          <g id="路径-13" transform="translate(0.000000, 21.167763)">
                            <polygon
                              id="路径-11"
                              points="13.9266941 1.26121336e-13 -1.17239551e-13 8.64947511 14.1532193 16.1404361 28.3064386 8.64947511"
                            />
                          </g>
                        </g>
                        <g
                          id="路径-12"
                          transform="translate(17.226836, 51.766822) rotate(23.000000) translate(-17.226836, -51.766822) translate(2.726836, 43.766822)"
                        >
                          <polygon
                            id="路径-11"
                            points="13.9266941 1.26121336e-13 -1.17239551e-13 8.53714427 14.1532193 15.9308201 28.3064386 8.53714427"
                          />
                        </g>
                      </g>
                      <g
                        id="路径-12"
                        transform="translate(19.825299, 46.693229) rotate(23.000000) translate(-19.825299, -46.693229) translate(5.325299, 38.693229)"
                      >
                        <polygon
                          id="路径-11"
                          points="13.9266941 1.26121336e-13 -1.17239551e-13 8.53714427 14.1532193 15.9308201 28.3064386 8.53714427"
                        />
                      </g>
                    </g>
                  </g>
                </g>
              </g>
            </g>
          </g>
        </svg>
      </div>
    </div>

    <div id="add">
      <div class="title">新增治愈和病亡病例</div>
      <div id="legend">
        <div class="legend_part">
          <div class="legend_line_cure"></div>
          <div class="legend_icon_line cure"></div>
          <div class="legend_text_line">治愈率</div>
        </div>
        <div class="legend_part">
          <div class="legend_line_death"></div>
          <div class="legend_icon_line death"></div>
          <div class="legend_text_line">病亡率</div>
        </div>
        <div class="legend_part">
          <div class="legend_icon cure"></div>
          <div class="legend_text">治愈人数</div>
        </div>
        <div class="legend_part">
          <div class="legend_icon death"></div>
          <div class="legend_text">病亡人数</div>
        </div>
      </div>

      <div id="country">
        <div class="title_1">全国</div>
        <div class="life_svg_div">
          <svg width="100%" height="100%">
            <g id="selected_background">
              <rect
                :x="add_x_begin + (date_select_id * 2 + 1) * add_x_step - add_x_step * 1.4"
                :y="add_y_begin"
                :width="add_x_step * 2.8"
                :height="add_y_step * 8.5"
                fill="rgba(0, 186, 209, 0.2)"
              />
              <rect
                :x="add_x_begin + (date_select_id * 2 + 1) * add_x_step - add_x_step * 1.1"
                :y="add_y_step * 6.2"
                :width="add_x_step * 2.2"
                :height="add_y_step * 0.6"
                :rx="add_y_step * 0.1"
                :ry="add_y_step * 0.1"
                fill="#00bad1"
              />
            </g>
            <g id="line-chart">
              <g id="line-y-label">
                <text style="font-size: 10px;">
                  <tspan style="text-anchor: end;" :x="add_x_begin-2" :y="add_y_begin+4">5%</tspan>
                  <tspan style="text-anchor: end;" :x="add_x_begin-2" :dy="add_y_step*2.5">0</tspan>
                </text>
              </g>
              <g id="line-y">
                <path
                  :d="`M${add_x_begin},${add_y_begin}h${add_svg_width - add_x_begin}`"
                  style="stroke: #6f6f6f; stroke-width: 1px;"
                />
                <path
                  :d="`M${add_x_begin},${add_y_step*3}h${add_svg_width - add_x_begin}`"
                  style="stroke: #6f6f6f; stroke-width: 1px;"
                />
              </g>
              <g id="line-node">
                <rect
                  v-for="(data, index) in cure_dataset"
                  width="5"
                  height="5"
                  class="cure"
                  :x="add_x_begin + (index * 2 + 1) * add_x_step - 2.5"
                  :y="add_y_begin + (0.05 - data.cure_rate) * add_y_step * 2.5 / 0.05 - 2.5"
                  :key="`${data.cure_rate}${index}`"
                />
                <rect
                  v-for="(data, index) in cure_dataset"
                  width="5"
                  height="5"
                  class="death"
                  :x="add_x_begin + (index * 2 + 1) * add_x_step - 2.5"
                  :y="add_y_begin + (0.05 - data.death_rate) * add_y_step * 2.5 / 0.05 - 2.5"
                  :key="`${data.death_rate}${index}`"
                />
              </g>
              <g id="line-path">
                <path :d="computed_path_death(cure_dataset)" fill="rgba(51, 51, 51, 0.1)" />
                <path :d="computed_path_cure(cure_dataset)" fill="rgba(121, 192, 155, 0.14)" />
                <path
                  style="stroke: #62c298; stroke-width: 1px; stroke-dasharray: 1, 1;"
                  fill="none"
                  :d="computed_path_cure_(cure_dataset)"
                />
                <path
                  style="stroke: #333333; stroke-width: 1px; stroke-dasharray: 1, 1;"
                  fill="none"
                  :d="computed_path_death_(cure_dataset)"
                />
              </g>
              <g id="selected">
                <text
                  text-anchor="middle"
                  style="font-size: 10px; fill: #888888;"
                  :x="add_x_begin + (date_select_id * 2 + 1) * add_x_step"
                  :y="add_y_begin + (0.05 - cure_dataset[date_select_id].cure_rate) * add_y_step * 2.5 / 0.05 - 5"
                >{{cure_dataset[date_select_id].cure_rate ? (cure_dataset[date_select_id].cure_rate * 100).toFixed(1) : '???'}}%</text>
                <text
                  text-anchor="middle"
                  style="font-size: 10px; fill: #888888;"
                  :x="add_x_begin + (date_select_id * 2 + 1) * add_x_step"
                  :y="add_y_begin + (0.05 - cure_dataset[date_select_id].death_rate) * add_y_step * 2.5 / 0.05 + 12"
                >{{cure_dataset[date_select_id].death_rate ? (cure_dataset[date_select_id].death_rate * 100).toFixed(1) : '???'}}%</text>
              </g>
            </g>
            <g id="bar-chart">
              <g id="bar-y-label">
                <text font-size="10" :y="add_y_begin + add_y_step * 2.5 + 4">
                  <tspan
                    v-for="(label, index) in add_bar_y_label"
                    :key="`${label}${index}`"
                    :x="index===5?(add_x_begin - 4):(add_x_begin - 2)"
                    :dy="add_y_step"
                    style="text-anchor: end;"
                  >{{num2text(label)}}</tspan>
                </text>
              </g>
              <g id="bar-y">
                <path
                  v-for="(label, index) in add_bar_y_label"
                  :key="`${label}${index}`"
                  :d="`M${add_x_begin},${add_y_begin + add_y_step * 3.5 + add_y_step * index}h${add_svg_width - add_x_begin}`"
                  :style="(index === 2 || index === 3) ? 'stroke: #6f6f6f; stroke-width: 1px;' : 'stroke: #6f6f6f; stroke-width: 0.3px;'"
                />
              </g>
              <g id="bar-rect-cure">
                <rect
                  v-for="(data, index) in cure_dataset"
                  :key="`bar-rect-cure-${data.cure}${index}`"
                  :x="add_x_begin + (0.5 + index * 2) * add_x_step"
                  :y="(1000-data.cure)/1000 * 2 * add_y_step + add_y_step * 4"
                  :width="add_x_step"
                  :height="data.cure/1000 * 2 * add_y_step"
                  class="cure"
                />
                <text
                  v-for="(data, index) in cure_dataset"
                  style="text-anchor: middle;"
                  font-size="10"
                  fill="#888888"
                  :x="add_x_begin + (1 + index * 2) * add_x_step"
                  :y="(1000-data.cure)/1000 * 2 * add_y_step + add_y_step * 4 - 2"
                  :key="`bar-rect-cure-text-${data.cure}${index}`"
                >{{num2text(data.cure)}}</text>
              </g>
              <g id="bar-rect-death">
                <rect
                  v-for="(data, index) in cure_dataset"
                  :key="`bar-rect-death${data.death}${index}`"
                  :x="add_x_begin + (0.5 + index * 2) * add_x_step"
                  :y="add_y_step * 7"
                  :width="add_x_step"
                  :height="data.death/400 * 2 * add_y_step"
                  class="death"
                />
                <text
                  v-for="(data, index) in cure_dataset"
                  style="text-anchor: middle;"
                  font-size="10"
                  fill="#888888"
                  :x="add_x_begin + (1 + index * 2) * add_x_step"
                  :y="add_y_step * 7 + data.death/400 * 2 * add_y_step + 10"
                  :key="`bar-rect-death-text-${data.death}${index}`"
                >{{num2text(data.death)}}</text>
              </g>
              <g id="bar-x-label">
                <text
                  v-for="(label, index) in date_list"
                  font-size="10"
                  font-weight="bold"
                  :fill="index===date_select_id ? 'white' : '#333333'"
                  style="text-anchor: middle;"
                  :key="`${label.month}-${label.day}-${index}`"
                  :x="add_x_begin + (1 + index * 2) * add_x_step"
                  :y="add_y_step * 6.6"
                >{{label.month}}/{{label.day}}</text>
              </g>
            </g>
          </svg>
        </div>
      </div>

      <div id="slider">
        <!-- <div>{{date_select_id}}</div> -->
        <svg id="slider_svg" width="100%" height="100%">
          <defs>
            <filter id="shadow">
              <feDropShadow dx="0" dy="0" stdDeviation="0.9" />
            </filter>
          </defs>
        </svg>
      </div>
    </div>
  </div>
</template>

<script>
import * as d3 from "d3";
export default {
  name: "life-and-death",
  data() {
    return {
      add_y_step: 0,
      add_y_begin: 0,
      add_x_step: 0,
      add_x_begin: 0,
      select_time: "2月6日",
      subscription_area: "湖北",
      dataset: [
        {
          title_1: "武汉",
          title_2: "",
          siwang: 362,
          zhiyu: 368,
          quezhen: 8351
          // quezhen: 10000
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
          title_2: "（除湖北）",
          siwang: 13,
          zhiyu: 401,
          quezhen: 7699
        }
      ],
      total_svg_width: 0,
      total_svg_height: 0,
      total_begin_x: 0,
      total_step_x: 0,
      total_x_label: [0, 200, 400, 600, 800, 1000, 7000, 10000],
      date_select_id: 0,

      add_svg_width: 0,
      add_svg_height: 0,
      cure_dataset: [
        {
          cure: 135,
          death: 20,
          diagnosis: 500
        }
      ],
      cure_dataset_1: [
        {
          cure: 135,
          death: 20,
          diagnosis: 500
        }
      ],
      add_bar_y_label: [1000, 500, 0, 0, 200, 400],

      country_dataset: [],
      date_list: Array(14).fill({ month: 1, day: 1 }),
      hubei_dataset: [],
      wuhan_dataset: []
    };
  },
  methods: {
    total_svg_g_style(index) {
      return `transform: translate(0, ${this.total_svg_height *
        0.28 *
        index}px);`;
    },
    total_bar_width(d) {
      if (d >= this.total_x_label[this.total_x_label.length - 2]) {
        let cal_d = d - this.total_x_label[this.total_x_label.length - 2];
        let scale_d =
          this.total_x_label[this.total_x_label.length - 1] -
          this.total_x_label[this.total_x_label.length - 2];
        let scale_width = this.total_step_x * 1.5;
        let cal_width = (cal_d / scale_d) * scale_width;
        return cal_width + this.total_step_x * (this.total_x_label.length - 2);
      } else {
        // console.log(d, this.total_x_label[this.total_x_label.length - 3], this.total_step_x, (this.total_x_label.length - 3))
        return (
          (d / this.total_x_label[this.total_x_label.length - 3]) *
          this.total_step_x *
          (this.total_x_label.length - 3)
        );
      }
    },
    num2text(num) {
      let result = "";
      if (num === 0) return "0";
      let t = 0;
      while (num > 0) {
        if (t == 3) {
          result += ",";
          t = 0;
        }
        result += num % 10;
        num = parseInt(num / 10);
        t++;
      }
      return result
        .split("")
        .reverse()
        .join("");
    },
    generate_data(n) {
      let result = [];
      for (let i = 0; i < n; i++) {
        let cure = 200 + Math.round(Math.random() * 600);
        let death = 50 + Math.round(Math.random() * 300);
        let diagnosis = 16000 + Math.round(Math.random() * 1000);
        let cure_rate = cure / diagnosis;
        let death_rate = death / diagnosis;
        result.push({
          cure,
          death,
          diagnosis,
          cure_rate,
          death_rate
        });
      }
      return result;
    },
    computed_path_cure(dataset) {
      let result = `M${this.add_x_begin + this.add_x_step},${this.add_y_begin +
        this.add_y_step * 2.5}`;
      dataset.forEach((data, index) => {
        result += `L${this.add_x_begin +
          (index * 2 + 1) * this.add_x_step},${this.add_y_begin +
          ((0.05 - data.cure_rate) * this.add_y_step * 2.5) / 0.05}`;
      });
      result += `L${this.add_x_begin +
        (dataset.length * 2 - 1) * this.add_x_step},${this.add_y_begin +
        this.add_y_step * 2.5}Z`;
      // console.log(result)
      return result;
    },
    computed_path_cure_(dataset) {
      let result = "";
      dataset.forEach((data, index) => {
        result += index === 0 ? "M" : "L";
        result += `${this.add_x_begin +
          (index * 2 + 1) * this.add_x_step},${this.add_y_begin +
          ((0.05 - data.cure_rate) * this.add_y_step * 2.5) / 0.05}`;
      });
      // console.log(result)
      return result;
    },
    computed_path_death(dataset) {
      let result = `M${this.add_x_begin + this.add_x_step},${this.add_y_begin +
        this.add_y_step * 2.5}`;
      dataset.forEach((data, index) => {
        result += `L${this.add_x_begin +
          (index * 2 + 1) * this.add_x_step},${this.add_y_begin +
          ((0.05 - data.death_rate) * this.add_y_step * 2.5) / 0.05}`;
      });
      result += `L${this.add_x_begin +
        (dataset.length * 2 - 1) * this.add_x_step},${this.add_y_begin +
        this.add_y_step * 2.5}Z`;
      // console.log(result)
      return result;
    },
    computed_path_death_(dataset) {
      let result = "";
      dataset.forEach((data, index) => {
        result += index === 0 ? "M" : "L";
        result += `${this.add_x_begin +
          (index * 2 + 1) * this.add_x_step},${this.add_y_begin +
          ((0.05 - data.death_rate) * this.add_y_step * 2.5) / 0.05}`;
      });
      // console.log(result)
      return result;
    }
  },
  mounted: async function() {
    let getDataUrl = "https://tanshaocong.github.io/2019-nCoV/map.csv";
    let data_tmp = await d3.csv(getDataUrl);
    let day_begin = 10;
    let month_begin = 1;

    //
    let country_dataset_ = [];
    data_tmp.forEach(data => {
      if (data["类别"] === "国家级") {
        let month = data["公开时间"].split("月")[0];
        let day = data["公开时间"].split("日")[0].split("月")[1];
        if (month > month_begin || (month == month_begin && day >= day_begin)) {
          country_dataset_.push({
            cure: data["新增治愈出院数"] ? +data["新增治愈出院数"] : 0,
            death: data["新增死亡数"] ? +data["新增死亡数"] : 0,
            diagnosis: data["新增确诊病例"] ? +data["新增确诊病例"] : 0,
            hejian: data["核减"] ? +data["核减"] : 0,
            month,
            day
          });
          let len = country_dataset_.length;
          country_dataset_[len - 1]["total_cure"] =
            len > 1 ? country_dataset_[len - 2]["total_cure"] : 0;
          country_dataset_[len - 1]["total_cure"] +=
            country_dataset_[len - 1]["cure"];
          country_dataset_[len - 1]["total_death"] =
            len > 1 ? country_dataset_[len - 2]["total_death"] : 0;
          country_dataset_[len - 1]["total_death"] +=
            country_dataset_[len - 1]["death"];
          country_dataset_[len - 1]["total_diagnosis"] =
            len > 1 ? country_dataset_[len - 2]["total_diagnosis"] : 0;
          country_dataset_[len - 1]["total_diagnosis"] +=
            country_dataset_[len - 1]["diagnosis"] +
            country_dataset_[len - 1]["hejian"];
          country_dataset_[len - 1]["cure_rate"] = country_dataset_[len - 1]["total_cure"] / country_dataset_[len - 1]["total_diagnosis"]
          country_dataset_[len - 1]["death_rate"] = country_dataset_[len - 1]["total_death"] / country_dataset_[len - 1]["total_diagnosis"]
        }
      }
    });

    // console.log(this.country_dataset)

    // data_hubei
    let hubei_dataset_ = [];
    data_tmp.forEach(data => {
      if (data["类别"] === "省级" && data["省份"] === "湖北") {
        let month = data["公开时间"].split("月")[0];
        let day = data["公开时间"].split("日")[0].split("月")[1];
        if (month > month_begin || (month == month_begin && day >= day_begin)) {
          hubei_dataset_.push({
            cure: data["新增治愈出院数"] ? +data["新增治愈出院数"] : 0,
            death: data["新增死亡数"] ? +data["新增死亡数"] : 0,
            diagnosis: data["新增确诊病例"] ? +data["新增确诊病例"] : 0,
            hejian: data["核减"] ? +data["核减"] : 0,
            month,
            day
          });
          let len = hubei_dataset_.length;
          hubei_dataset_[len - 1]["total_cure"] =
            len > 1 ? hubei_dataset_[len - 2]["total_cure"] : 0;
          hubei_dataset_[len - 1]["total_cure"] +=
            hubei_dataset_[len - 1]["cure"];
          hubei_dataset_[len - 1]["total_death"] =
            len > 1 ? hubei_dataset_[len - 2]["total_death"] : 0;
          hubei_dataset_[len - 1]["total_death"] +=
            hubei_dataset_[len - 1]["death"];
          hubei_dataset_[len - 1]["total_diagnosis"] =
            len > 1 ? hubei_dataset_[len - 2]["total_diagnosis"] : 0;
          hubei_dataset_[len - 1]["total_diagnosis"] +=
            hubei_dataset_[len - 1]["diagnosis"] +
            hubei_dataset_[len - 1]["hejian"];
        }
      }
    });
    // console.log('country_dataset_', country_dataset_)

    // console.log(this.hubei_dataset)

    // data_wuhan
    let wuhan_dataset_ = [];
    data_tmp.forEach(data => {
      if (
        data["类别"] === "地区级" &&
        data["省份"] === "湖北" &&
        data["城市"] === "武汉"
      ) {
        let month = data["公开时间"].split("月")[0];
        let day = data["公开时间"].split("日")[0].split("月")[1];
        if (month > month_begin || (month == month_begin && day >= day_begin)) {
          wuhan_dataset_.push({
            cure: data["新增治愈出院数"] ? +data["新增治愈出院数"] : 0,
            death: data["新增死亡数"] ? +data["新增死亡数"] : 0,
            diagnosis: data["新增确诊病例"] ? +data["新增确诊病例"] : 0,
            hejian: data["核减"] ? +data["核减"] : 0,
            month,
            day
          });
          let len = wuhan_dataset_.length;
          wuhan_dataset_[len - 1]["total_cure"] =
            len > 1 ? wuhan_dataset_[len - 2]["total_cure"] : 0;
          wuhan_dataset_[len - 1]["total_cure"] +=
            wuhan_dataset_[len - 1]["cure"];
          wuhan_dataset_[len - 1]["total_death"] =
            len > 1 ? wuhan_dataset_[len - 2]["total_death"] : 0;
          wuhan_dataset_[len - 1]["total_death"] +=
            wuhan_dataset_[len - 1]["death"];
          wuhan_dataset_[len - 1]["total_diagnosis"] =
            len > 1 ? wuhan_dataset_[len - 2]["total_diagnosis"] : 0;
          wuhan_dataset_[len - 1]["total_diagnosis"] +=
            wuhan_dataset_[len - 1]["diagnosis"] +
            wuhan_dataset_[len - 1]["hejian"];
        }
      }
    });
    // console.log('country_dataset_', country_dataset_)
    this.wuhan_dataset = wuhan_dataset_.splice(wuhan_dataset_.length - 14, 14);
    this.hubei_dataset = hubei_dataset_.splice(hubei_dataset_.length - 14, 14);
    this.country_dataset = country_dataset_.splice(
      country_dataset_.length - 14,
      14
    );
    // console.log(this.wuhan_dataset)

    // date_list
    let date_list = [];
    this.country_dataset.forEach(d => {
      date_list.push({
        month: d.month,
        day: d.day
      });
    });
    this.date_list = date_list;
    
    this.cure_dataset = this.country_dataset
    // console.log(this.cure_dataset)

    let total_dataset = [
      {
        title_1: "武汉",
        title_2: "",
        siwang: [],
        zhiyu: [],
        quezhen: [],
      },
      {
        title_1: "湖北",
        title_2: "（除武汉）",
        siwang: [],
        zhiyu: [],
        quezhen: [],
      },
      {
        title_1: "全国",
        title_2: "（除湖北）",
        siwang: [],
        zhiyu: [],
        quezhen: [],
      }
    ]
    for (let i = 0; i<this.country_dataset.length; i++) {
      total_dataset[0].siwang.push()
    }



    // this.cure_dataset = this.generate_data(14);
    let total_svg_div_rect = d3
      .select("#total_svg_div")
      .node()
      .getBoundingClientRect();
    this.total_svg_width = total_svg_div_rect.width;
    this.total_svg_height = total_svg_div_rect.height;
    this.total_begin_x = 55;
    this.total_step_x =
      (total_svg_div_rect.width - this.total_begin_x) /
      this.total_x_label.length;
    // console.log("total_svg_div_rect", total_svg_div_rect);

    this.date_select_id = this.date_list.length - 1;
    let that = this;
    let DRAGWIDTH = total_svg_div_rect.width;
    let DRAGHEIGHT = 40;
    let MARGIN = {
      left: 10,
      right: 10,
      top: 10,
      bottom: 10
    };
    let plotDragBars = function(svgId, total) {
      let svg = d3.select(`#${svgId}`);
      // svg.attr("height", DRAGHEIGHT).attr("width", DRAGWIDTH);
      let canvas = svg
        .append("g")
        .attr("transform", `translate(${MARGIN.left}, ${MARGIN.top})`);
      let width = DRAGWIDTH - MARGIN.left - MARGIN.right;
      let height = DRAGHEIGHT - MARGIN.top - MARGIN.bottom;
      // let width = total_svg_div_rect.width;
      // let height = 30;
      let w = width / total;
      let h = 15;
      let timeScale = d3
        .scaleLinear()
        .range([0, width - w / 2])
        .domain([0, total - 1]);
      let g = canvas.append("g");
      g.append("line")
        .attr("x2", width)
        .attr("y1", height / 2)
        .attr("y2", height / 2)
        .classed("slider-container", true);
      let target = g
        .append("rect")
        .attr("x", w * total - w)
        .attr("y", height / 2 - h / 2)
        .attr("width", w)
        .attr("height", h)
        .attr("rx", 3)
        .attr("ry", 3)
        .classed("slider-rect", true);
      target.call(
        d3
          .drag()
          .on("drag", function() {
            let x = Math.min(Math.max(0, d3.event.x), width - w / 2);
            let self = d3.select(this);
            self.attr("x", x);
            let timeIdx = Math.round(timeScale.invert(x));
            let position = timeIdx * w;
            self.attr("x", position);
            that.date_select_id = timeIdx;
          })
          .on("end", function() {
            // let x = Math.min(Math.max(0, d3.event.x), width);
            // let self = d3.select(this);
            // let timeIdx = Math.round(timeScale.invert(x));
            // let position = timeIdx * w;
            // self.attr("x", position);
            // that.date_select_id = timeIdx;
            // updateView(timeIdx);
          })
      );
    };
    let svgId = "slider_svg";
    plotDragBars(svgId, this.date_list.length);

    let add_div_rect = d3
      .select(".life_svg_div")
      .node()
      .getBoundingClientRect();
    // console.log(add_div_rect)
    this.add_svg_width = add_div_rect.width;
    this.add_svg_height = add_div_rect.height;
    this.add_y_step = this.add_svg_height / 9.5;
    this.add_y_begin = this.add_y_step * 0.5;
    // console.log('this.add_y_begin', this.add_y_begin)
    this.add_x_begin = 30;
    this.add_x_step =
      (this.add_svg_width - this.add_x_begin - 10) /
      2 /
      this.cure_dataset.length;

  },
  computed: {
    total_dataset() {
      let wuhan = {
        title_1: "武汉",
        title_2: "",
        siwang: this.wuhan_dataset[this.date_select_id]
          ? this.wuhan_dataset[this.date_select_id]["total_death"]
          : 0,
        zhiyu: this.wuhan_dataset[this.date_select_id]
          ? this.wuhan_dataset[this.date_select_id]["total_cure"]
          : 0,
        quezhen: this.wuhan_dataset[this.date_select_id]
          ? this.wuhan_dataset[this.date_select_id]["total_diagnosis"]
          : 0
      };
      let hubei = {
        title_1: "湖北",
        title_2: "（除武汉）",
        siwang: this.hubei_dataset[this.date_select_id]
          ? this.hubei_dataset[this.date_select_id]["total_death"] -
            this.wuhan_dataset[this.date_select_id]["total_death"]
          : 0,
        zhiyu: this.hubei_dataset[this.date_select_id]
          ? this.hubei_dataset[this.date_select_id]["total_cure"] -
            this.wuhan_dataset[this.date_select_id]["total_cure"]
          : 0,
        quezhen: this.hubei_dataset[this.date_select_id]
          ? this.hubei_dataset[this.date_select_id]["total_diagnosis"] -
            this.wuhan_dataset[this.date_select_id]["total_diagnosis"]
          : 0
      };
      let quanguo = {
        title_1: "全国",
        title_2: "（除湖北）",
        siwang: this.country_dataset[this.date_select_id]
          ? this.country_dataset[this.date_select_id]["total_death"] -
            this.hubei_dataset[this.date_select_id]["total_death"]
          : 0,
        zhiyu: this.country_dataset[this.date_select_id]
          ? this.country_dataset[this.date_select_id]["total_cure"] -
            this.hubei_dataset[this.date_select_id]["total_cure"]
          : 0,
        quezhen: this.country_dataset[this.date_select_id]
          ? this.country_dataset[this.date_select_id]["total_diagnosis"] -
            this.hubei_dataset[this.date_select_id]["total_diagnosis"]
          : 0
      };
      let res = [wuhan, hubei, quanguo]
      console.log('res', res)
      return res;
      // let res = []
      // res.push(this.country_dataset)
    }
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

#head {
  margin-top: 40px;
  vertical-align: middle;
  #left_border {
    margin-top: 4px;
    height: 22px;
    width: 5px;
    border-radius: 2.5px;
    background: #00bad1;
    float: left;
  }
  #title {
    margin-left: 16px;
    font-size: 24px;
    font-weight: 600;
    color: #333333;
  }
  #description {
    margin-top: 5px;
    margin-left: 18px;
    font-size: 14px;
    color: #888888;
  }
}

#explanation {
  // position: relative;
  margin-top: 20px;
  height: 100%;
  // border: 1px solid red;
  #explanation_text {
    position: relative;
    top: 0px;
    line-height: 18px;
    font-size: 14px;
    // border: 1px solid green;
    padding: 20px 25px 25px 25px;
    background: #f7f7f7;
    box-shadow: 1px 1px 1px rgba(0, 0, 0, 0.2);
    color: #888888;
  }
}

.title {
  font-weight: bold;
  font-size: 18px;
}

.title_1 {
  font-weight: bold;
  font-size: 16px;
}

#total {
  margin-top: 30px;
  #legend {
    margin-top: 10px;
    height: 20px;
    .legend_part {
      float: left;
      margin-left: 40px;
      .legend_text {
        float: left;
        margin-left: 10px;
        font-size: 14px;
      }
    }
  }
  #total_svg_div {
    margin-top: 10px;
    width: 100%;
    height: 40vw;
    // background: rgba(142, 170, 142, 0.2);
    // #total_svg {

    // }
    .total_label_line {
      stroke-width: 0.5px;
      stroke: #6f6f6f;
    }
  }
}

.icon {
  width: 10px;
  height: 10px;
  float: left;
  margin-top: 3px;
}

.diagnosis {
  // fill: #9a0000;
  // background: #9a0000;
  // color: #9a0000;
  // opacity: 0.69;
  fill: #de5e5b;
  background: #de5e5b;
  color: #de5e5b;
}

.cure {
  fill: #62c298;
  background: #62c298;
  color: #62c298;
}

.death {
  fill: #010604;
  background: #010604;
  color: #010604;
}

.bar_text {
  font-size: 12px;
  fill: #ffffff;
}

.label_text {
  font-size: 12px;
  fill: #919191;
  text-anchor: middle;
}

#add {
  margin-top: 30px;
  #legend {
    margin-top: 10px;
    width: 100%;
    height: 40px;
    // background: rgba(142, 170, 142, 0.1);
    .legend_part {
      vertical-align: middle;
      // text-align: center;
      position: relative;
      width: 25%;
      height: 100%;
      display: inline-block;
    }
    .legend_line_cure {
      position: absolute;
      top: 50%;
      left: 15px;
      transform: translateY(-50%);
      width: 20px;
      height: 1px;
      border-bottom: 1px dashed #62c298;
    }
    .legend_line_death {
      position: absolute;
      top: 50%;
      left: 15px;
      transform: translateY(-50%);
      width: 20px;
      height: 1px;
      border-bottom: 1px dashed #010604;
    }
    .legend_icon_line {
      position: absolute;
      top: 50%;
      left: 35px;
      transform: translateY(-50%);
      width: 8px;
      height: 8px;
    }
    .legend_icon {
      position: absolute;
      top: 50%;
      left: 15px;
      transform: translateY(-50%);
      width: 14px;
      height: 14px;
    }
    .legend_text_line {
      position: absolute;
      top: 50%;
      left: 50px;
      transform: translateY(-50%);
      font-size: 12px;
      height: 13px;
      width: 50px;
    }
    .legend_text {
      position: absolute;
      top: 50%;
      left: 35px;
      transform: translateY(-50%);
      font-size: 12px;
      height: 13px;
      width: 50px;
    }
  }
  .life_svg_div {
    margin-top: 10px;
    width: 100%;
    height: 70vw;
    // background: rgba(142, 170, 142, 0.1);
  }
  #country {
    margin-top: 20px;
  }
  #subscription {
    margin-top: 20px;
  }
  #slider {
    margin-top: 20px;
    margin-bottom: 200px;
    width: 100%;
    height: 50px;
    // background: rgb(142, 170, 142);
  }
}

.slider-container {
  stroke: #ececec;
  stroke-width: 10px;
  stroke-linecap: round;
}

.slider-rect {
  box-shadow: 0 0 6px 0 rgba(0, 0, 0, 0.5);
  fill: #00bad1;
  filter: url(#shadow);
}
</style>