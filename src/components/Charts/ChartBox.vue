<template>
  <div class="border border-gray-200 bg-white rounded-lg py-4">
    <EChartComponent
      :title="title"
      :secondParametr="secondParametr"
      :firstParametr="firstParametr"
      :yAxisData="yAxisData"
    />
  </div>
</template>
<script setup>
import { defineProps } from "vue";
import EChartComponent from "@/components/Charts/EChartComponent.vue";
defineProps({
  title: {
    type: String,
    default: "",
  },
  firstParametr: {
    type: Array,
    default: null
  },
  secondParametr: {
    type: Array,
    default: null
  },
  yAxisData: {
    type: Array,
    default: null
  }
});
</script>

<style scoped></style>
