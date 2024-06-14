<template>
  <div class="border border-gray-200 bg-white rounded-lg py-4">
    <EChartComponent :title="title" />
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
});
</script>

<style scoped></style>
