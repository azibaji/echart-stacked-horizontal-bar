<template>
  <div class="p-4 bg-gray-200 lg:h-screen lg:pt-20">
    <div class="grid lg:grid-cols-3 mx-auto gap-3">
      <chart-box
        v-for="n in 3"
        :key="n"
        :title="`DND Detention Free Time ${n}`"
        :secondParametr="secondParametr"
        :firstParametr= "firstParametr"
      />
    </div>
  </div>
</template>

<script setup>
import {ref} from 'vue'
const firstParametr = ref([5, 20, 36, 10, 10, 20, 30, 40, 10, 15, 25, 5])
const secondParametr = ref( [15, 25, 16, 20, 30, 10, 20, 5, 10, 15, 25, 5])
import ChartBox from "./components/Charts/ChartBox.vue";
</script>
