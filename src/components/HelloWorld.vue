<template>
  <div>
    <el-button type="primary" @click="onChange">Change</el-button>
    <div id="content_publish_echar" style="width: 600px; height: 600px"></div>
  </div>
</template>
<script setup lang="ts">
// #region echars引用相关
import * as echarts from "echarts/core";
import {
  GridComponent,
  GridComponentOption,
  TooltipComponent,
  TooltipComponentOption,
} from "echarts/components";
import { BarChart, BarSeriesOption } from "echarts/charts";
import { CanvasRenderer, SVGRenderer } from "echarts/renderers";
import { onMounted, reactive } from "vue";

echarts.use([GridComponent, TooltipComponent, BarChart, SVGRenderer]);

type EChartsOption = echarts.ComposeOption<
  GridComponentOption | BarSeriesOption | TooltipComponentOption
>;

// #endregion

interface IState {
  echars: any;
}
const state = reactive<IState>({
  echars: null,
});

const initPublishContentEchar = () => {
  const chartDom = document.getElementById("content_publish_echar");
  if (chartDom) {
    // eslint-disable-next-line prefer-const
    let myChart = echarts.init(chartDom);
    // state.echars.push(myChart)
    state.echars = myChart;
    // eslint-disable-next-line prefer-const
    let option: EChartsOption = {
      grid: {
        left: "3%",
        right: "4%",
        bottom: "10%",
        top: "10%",
        containLabel: true,
      },
      xAxis: [
        {
          type: "category",
          data: ["Mon", "Tue", "Wed", "Thu", "Fri", "Sat", "Sun"],
          axisTick: {
            interval: 0,
            alignWithLabel: true,
            show: false,
          },
          nameLocation: "middle",
          splitNumber: 35,
          axisLine: {
            lineStyle: {
              color: "rgba(15, 192, 255, 0.3)",
            },
          },
          axisLabel: {
            color: "#666666", // X轴文字颜色
          },
        },
      ],
      yAxis: [
        {
          type: "value",
          axisLine: {
            lineStyle: {
              color: "#fff",
            },
          },
          splitLine: {
            show: true,
            lineStyle: {
              color: "rgba(15, 192, 255, 0.3)",
            },
          },
          axisLabel: {
            color: "#666666", // X轴文字颜色
          },
        },
      ],
      series: [
        {
          name: "a",
          data: [120, 200, 150, 80, 70, 110, 130],
          type: "bar",
          stack: "item",
          barWidth: "20%",
        },
        {
          name: "b",
          data: [120, 200, 150, 80, 70, 110, 130],
          type: "bar",
          stack: "item",
          barWidth: "20%",
        },
      ],
      tooltip: [
        {
          trigger: "axis",
        },
      ],
    };

    myChart.setOption(option);
  }
};

const onChange = () => {
  let options = {
    xAxis: [
      {
        axisLine: {
          lineStyle: {
            color: "#FF0000",
          },
        },
        axisLabel: {
          color: "#FF0000", // X轴文字颜色
        },
      },
    ],
    yAxis: [
      {
        splitLine: {
          show: true,
          lineStyle: {
            color: "#FF0000",
          },
        },
        axisLabel: {
          color: "#FF0000", // X轴文字颜色
        },
      },
    ],
  };
  state.echars.setOption(options);
};

onMounted(() => {
  initPublishContentEchar();
});
</script>
