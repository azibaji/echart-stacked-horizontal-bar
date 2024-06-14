<template>
  <div class="chart-container">
    <div class="chart-wrapper">
      <div
        ref="chart"
        class="chart"
        :style="{ height: chartHeight + 'px' }"
      ></div>
    </div>

    <div class="custom-legend border-t border-gray-200 pt-4">
      <div
        v-for="(item, index) in legendData"
        :key="index"
        class="custom-legend-item"
        @click="toggleSeries(index)"
        :style="{ color: item.color }"
      >
        <span
          class="legend-marker"
          :style="{ backgroundColor: item.color }"
        ></span>
        {{ item.name }}
      </div>
    </div>
  </div>
</template>

<script setup>
import {
  ref,
  onMounted,
  onBeforeUnmount,
  defineProps,
  reactive,
  computed,
} from "vue";
import * as echarts from "echarts";

const chart = ref(null);
let myChart;
const legendData = reactive([
  { name: "Exceeded free-time period", color: "#155790", visible: true },
  {
    name: "Remaining free time days less or equal then 5",
    color: "#6bc85d",
    visible: true,
  },
]);

const props = defineProps({
  title: {
    type: String,
    default: "",
  },
});
const yAxisData = [
  "BEANR",
  "AUBNE",
  "ESBCN",
  "FRLEH",
  "PHBTG",
  "test1",
  "test2",
  "test3",
  "test4",
  "test5",
  "test6",
  "test7",
];

const chartHeight = computed(() => {
  const baseHeight = 330;
  const barCount = yAxisData.length;
  const additionalHeight = (barCount - 10) * 30; 
  return barCount > 10 ? baseHeight + additionalHeight : baseHeight;
});

const addLegendClass = () => {
  const legendContainer = chart.value.querySelector(".echarts-legend");
  if (legendContainer) {
    legendContainer.classList.add("custom-legend-style");
  }
};

onMounted(() => {
  myChart = echarts.init(chart.value);
  myChart.setOption({
    title: {
      text: props.title,
    },
    tooltip: {
      trigger: "axis",
      axisPointer: {
        type: "shadow",
      },
    },
    legend: {
      show: false,
    },
    grid: {
      left: "15%",
      right: "4%",
      bottom: "5%",
      containLabel: true,
    },
    xAxis: {
      name: "Horizontal Axis Label", 
      nameLocation: "center",
      nameTextStyle: {
        fontSize: 14,
        padding: [10, 0, 0, 0],
      },
      axisLine: {
        show: false,
      },
      axisTick: {
        show: false, 
      },
      splitLine: {
        show: false,
      },
      axisLabel: {
        show: true,
        margin: 20,
        formatter: function () {
          return ""; 
        },
      },
    },
    yAxis: {
      name: "Vertical Axis Label",
      nameLocation: "middle",
      nameRotate: 90,
      data: yAxisData,
      nameTextStyle: {
        fontSize: 14,
        padding: [0, 0, 70, 0],
      },
      axisLine: {
        show: false,
      },
      axisTick: {
        show: false, 
      },
      splitLine: {
        show: false,
        margin: 20, 
      },
      axisLabel: {
        show: true,
        margin: 10,
      },
    },
    series: [
      {
        type: "bar",
        data: Array(yAxisData.length).fill(100),
        itemStyle: {
          color: "#fafbfe",
        },
        barWidth: 20,
        silent: true,
        label: {
          show: false,
        },
        z: 1,
      },
      {
        name: "Exceeded free-time period",
        type: "bar",
        stack: "total",
        data: [5, 20, 36, 10, 10, 20, 30, 40, 10, 15, 25, 5],
        label: {
          show: true,
          position: "inside",
          verticalAlign: "middle",
          align: "center",
          formatter: "{c}",
          color: "#fff",
          fontWeight: "bold",
        },
        itemStyle: {
          color: "#155790",
          borderRadius: [2, 2, 2, 2],
        },
        barWidth: 20,
        z: 2, 
      },
      {
        name: "Gap",
        type: "bar",
        stack: "total",
        itemStyle: {
          color: "transparent",
        },
        data: Array(yAxisData.length).fill(2),
        barWidth: "10%", 
        barGap: "0%",
        tooltip: {
          show: false,
        },
        barwidth: 20,
        z: 2,
      },
      {
        name: "Remaining free time days less or equal to 5",
        type: "bar",
        stack: "total",
        data: [15, 25, 16, 20, 30, 10, 20, 5, 10, 15, 25, 5],
        label: {
          show: true,
          position: "inside",
          verticalAlign: "middle",
          align: "center",
          formatter: "{c}",
          color: "#fff",
          fontWeight: "bold",
        },
        itemStyle: {
          color: "#6bc85d",
          borderRadius: [2, 2, 2, 2],
        },
        barWidth: 20,
        z: 2, 
      },
    ],
    barGap: "-100%",
    barCategoryGap: "30%",
  });
  myChart.on("finished", addLegendClass);
  window.addEventListener("resize", myChart.resize);
});

onBeforeUnmount(() => {
  if (myChart) {
    window.removeEventListener("resize", myChart.resize);
    myChart.off("finished", addLegendClass);
    myChart.dispose();
  }
});
</script>

<style scoped>
.chart-container {
  width: 100%;
  text-align: center;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-between;
}
.chart-wrapper {
  width: 80%;
  height: 300px;
  overflow-y: auto;
  margin-bottom: 20px;
}
.chart {
  width: 100%;
}

.custom-legend {
  display: flex;
  justify-content: center;
  margin-top: 10px;
}

.custom-legend-item {
  margin: 0 10px;
  cursor: pointer;
  display: flex;
  align-items: flex-start;
  text-align: left;
  justify-content: flex-start;
  font-size: 13px;
}

.legend-marker {
  width: 12px;
  height: 12px;
  margin-right: 4px;
  margin-top: 4px;
  display: inline-block;
}
</style>
