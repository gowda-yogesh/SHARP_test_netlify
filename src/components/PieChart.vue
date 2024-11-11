<template>
    <Pie :data="chartConfig" :options="options" />
</template>
  
<script setup lang="ts">
import { Chart as ChartJS, ArcElement, Tooltip, Legend } from 'chart.js'
import { Pie } from 'vue-chartjs'

ChartJS.register(ArcElement, Tooltip, Legend)

const chartConfig = {
    labels: ['VueJs', 'EmberJs', 'ReactJs', 'AngularJs'],
    datasets: [
      {
        backgroundColor: ['#FFDD33', '#80DBFF', '#FF5C8D', '#CD8AF9', '#FBA04B', '#49D49D'],
        data: [40, 20, 80, 10]
      }
    ]
  }
  
const options = {
    responsive: true,
    maintainAspectRatio: false
}

</script>

  