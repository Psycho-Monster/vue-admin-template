<template>
  <div class="dashboard-container">
    <!-- <div class="dashboard-text">name: {{ name }}</div> -->
    <div class="top">
      <div class="card">
        <el-card class="box-card">
          <div slot="header" class="clearfix">
            <span>商品总量</span>
          </div>
          <div class="text item">
            <div class="count">1,128,163个</div>
            <div class="week">周同比 15% <span class="down">↓</span></div>
            <div class="day">日同比 10% <span class="up">↑</span></div>
          </div>
        </el-card>
      </div>
      <div class="line"></div>
    </div>
    <div class="bottom">
      <el-tabs v-model="activeName" @tab-click="handleClick">
        <el-tab-pane label="访问量" name="first">
          <div class="visits">
            <el-card class="box-card">
              <div slot="header" class="clearfix">
                <span>访问趋势</span>
              </div>
              <div class="text item">
                <div class="bar"></div>
              </div>
            </el-card>
            <div class="block">
              <el-card class="box-card">
                <div slot="header" class="clearfix">
                  <span>任务</span>
                </div>
                <div class="text item">
                  <el-timeline :reverse="reverse">
                    <el-timeline-item
                      v-for="(activity, index) in activities"
                      :key="index"
                      :timestamp="activity.timestamp"
                      :color="activity.color"
                      hide-timestamp
                    >
                      {{ activity.content }}
                    </el-timeline-item>
                  </el-timeline>
                </div>
              </el-card>
            </div>
          </div>
        </el-tab-pane>
        <el-tab-pane label="销售量" name="second">
          <div class="visits">
            <el-card class="box-card">
              <div slot="header" class="clearfix">
                <span>销售趋势</span>
              </div>
              <div class="text item">
                <div class="bar"></div>
              </div>
            </el-card>
            <div class="block">
              <el-card class="box-card">
                <div slot="header" class="clearfix">
                  <span>任务</span>
                </div>
                <div class="text item">
                  <el-timeline :reverse="reverse">
                    <el-timeline-item
                      v-for="(activity, index) in activities"
                      :key="index"
                      :timestamp="activity.timestamp"
                      :color="activity.color"
                      hide-timestamp
                    >
                      {{ activity.content }}
                    </el-timeline-item>
                  </el-timeline>
                </div>
              </el-card>
            </div>
          </div>
        </el-tab-pane>
      </el-tabs>
    </div>
  </div>
</template>

<script>
import { mapGetters } from "vuex";

export default {
  name: "Dashboard",
  data() {
    return {
      activeName: "first",
      reverse: false,
      activities: [
        {
          content: "新版本迭代会",
          timestamp: "2018-04-11",
          color: "#0bbd87",
        },
        {
          content: "完成网站设计初版",
          timestamp: "2018-04-13",
          color: "#0bbd87",
        },
        {
          content: "联调接口 功能验收",
          timestamp: "2018-04-15",
          color: "coral",
        },
        {
          content: "登录功能设计",
          timestamp: "2018-04-17",
          color: "#0bbd87",
        },
        {
          content: "权限验证",
          timestamp: "2018-04-19",
          color: "#0bbd87",
        },
        {
          content: "页面排版",
          timestamp: "2018-04-21",
        },
      ],
    };
  },
  mounted() {
    this.initBar();
    this.initLine();
  },
  computed: {
    ...mapGetters(["name"]),
  },
  methods: {
    handleClick(tab, event) {
      console.log(tab, event);
    },
    initBar() {
      const myChart = this.$echarts.init(document.querySelector(".bar"));
      const option = {
        color: ["#3398DB"],
        tooltip: {
          trigger: "axis",
          axisPointer: {
            // 坐标轴指示器，坐标轴触发有效
            type: "shadow", // 默认为直线，可选为：'line' | 'shadow'
          },
        },
        grid: {
          left: "3%",
          right: "4%",
          bottom: "3%",
          containLabel: true,
        },
        xAxis: [
          {
            type: "category",
            data: ["Mon", "Tue", "Wed", "Thu", "Fri", "Sat", "Sun"],
            axisTick: {
              alignWithLabel: true,
            },
          },
        ],
        yAxis: [
          {
            type: "value",
          },
        ],
        series: [
          {
            name: "直接访问",
            type: "bar",
            barWidth: "60%",
            data: [10, 52, 200, 334, 390, 330, 220],
          },
        ],
      };
      myChart.setOption(option);
    },
    initLine() {
      const myChart = this.$echarts.init(document.querySelector(".line"));
      const option = {
        tooltip: {
          trigger: "axis",
          axisPointer: {
            type: "cross",
            label: {
              backgroundColor: "#6a7985",
            },
          },
        },
        grid: {
          left: "3%",
          right: "4%",
          bottom: "3%",
          containLabel: true,
        },
        xAxis: [
          {
            type: "category",
            boundaryGap: false,
            data: ["周一", "周二", "周三", "周四", "周五", "周六", "周日"],
          },
        ],
        yAxis: [
          {
            type: "value",
          },
        ],
        series: [
          {
            name: "邮件营销",
            type: "line",
            stack: "总量",
            areaStyle: {},
            data: [120, 132, 101, 134, 90, 230, 210],
          },
          {
            name: "联盟广告",
            type: "line",
            stack: "总量",
            areaStyle: {},
            data: [220, 182, 191, 234, 290, 330, 310],
          },
          {
            name: "视频广告",
            type: "line",
            stack: "总量",
            areaStyle: {},
            data: [150, 232, 201, 154, 190, 330, 410],
          },
          {
            name: "直接访问",
            type: "line",
            stack: "总量",
            areaStyle: {},
            data: [320, 332, 301, 334, 390, 330, 320],
          },
          {
            name: "搜索引擎",
            type: "line",
            stack: "总量",
            label: {
              normal: {
                show: true,
                position: "top",
              },
            },
            areaStyle: {},
            data: [820, 932, 901, 934, 1290, 1330, 1320],
          },
        ],
      };

      myChart.setOption(option);
    },
  },
};
</script>

<style lang="scss" scoped>
.dashboard {
  &-container {
    margin: 30px;
  }
  &-text {
    font-size: 30px;
    line-height: 46px;
  }
}
.top {
  display: flex;
  justify-content: space-between;
}
.top .card {
  .text {
    font-size: 14px;
  }

  .item {
    margin-bottom: 18px;
  }

  .clearfix:before,
  .clearfix:after {
    display: table;
    content: "";
  }
  .clearfix:after {
    clear: both;
  }

  .box-card {
    width: 480px;
  }
}
.top .line {
  // flex: 1;
  width: 500px;
  height: 220px;
}
.visits {
  display: flex;
  justify-content: space-between;
}
.visits .bar {
  width: 500px;
  height: 200px;
}
.visits .block {
  width: 300px;
  padding-top: 1px;
  align-self: center;
}
.count {
  font-size: 30px;
  font-weight: bolder;
}
.week {
  margin: 10px 0;
}
.down {
  color: red;
}
.up {
  color: green;
}
</style>
