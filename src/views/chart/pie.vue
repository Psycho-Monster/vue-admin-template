<template>
  <div id="pie"></div>
</template>

<script>
export default {
  mounted() {
    this.initBar();
  },
  methods: {
    initBar() {
      const myChart = this.$echarts.init(document.getElementById("pie"));
      const option = {
        title: {
          left: "center",
        },
        legend: {
          left: "center",
          top: "bottom",
          data: [
            "rose1",
            "rose2",
            "rose3",
            "rose4",
            "rose5",
            "rose6",
            "rose7",
            "rose8",
          ],
        },
        series: [
          {
            name: "半径模式",
            type: "pie",
            radius: [20, 110],
            center: ["25%", "50%"],
            roseType: "radius",
            label: {
              show: false,
            },
            emphasis: {
              label: {
                show: true,
              },
            },
            data: [
              { value: 10, name: "rose1" },
              { value: 5, name: "rose2" },
              { value: 15, name: "rose3" },
              { value: 25, name: "rose4" },
              { value: 20, name: "rose5" },
              { value: 35, name: "rose6" },
              { value: 30, name: "rose7" },
              { value: 40, name: "rose8" },
            ],
          },
          {
            name: "面积模式",
            type: "pie",
            radius: [30, 110],
            center: ["75%", "50%"],
            roseType: "area",
            data: [
              { value: 10, name: "rose1" },
              { value: 5, name: "rose2" },
              { value: 15, name: "rose3" },
              { value: 25, name: "rose4" },
              { value: 20, name: "rose5" },
              { value: 35, name: "rose6" },
              { value: 30, name: "rose7" },
              { value: 40, name: "rose8" },
            ],
          },
        ],
      };

      myChart.setOption(option);
    },
  },
};
</script>

<style>
#pie {
  width: 600px;
  height: 400px;
  margin: 0 auto;
}
</style>