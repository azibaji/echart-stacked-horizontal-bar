<template>
  <div class="p-4 bg-gray-200 lg:h-screen lg:pt-20">
    <div class="grid lg:grid-cols-3 mx-auto gap-3">
      <chart-box
        v-for="n in 3"
        :key="n"
        :title="`DND Detention Free Time ${n}`"
      />
    </div>
  </div>
</template>

<script setup>
import ChartBox from "./components/Charts/ChartBox.vue";
</script>
