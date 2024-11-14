<template>
  <div class="chart-container">
    <Bar :data="data" :options="options" />
  </div>
</template>

<script lang="ts" setup>
import {
  BarElement,
  CategoryScale,
  Chart as ChartJS,
  Legend,
  LinearScale,
  Title,
  Tooltip,
} from "chart.js";
import { computed } from "vue";
import { Bar } from "vue-chartjs";

ChartJS.register(
  CategoryScale,
  LinearScale,
  BarElement,
  Title,
  Tooltip,
  Legend
);

// Define props to accept only `barChartData`
const props = defineProps({
  barChartData: {
    type: Object,
    required: true,
  },
});

// Extract overall analysis data for chart
const overallAnalysis = props.barChartData;

console.log("BarChart.vue : overallAnalysis", overallAnalysis);

// Reactive data for the bar chart
const data = computed(() => ({
  labels: ["high", "medium", "low"],
  datasets: [
    {
      label: 'SHARP analysis',
      backgroundColor: ["#BA3030", "#FBA04B", "#FFDD33"],
      data: [
        overallAnalysis.high || 0,
        overallAnalysis.medium || 0,
        overallAnalysis.low || 0,
      ],
    },
  ],
}));

// Enhanced chart options
const options = {
  responsive: true,
  plugins: {
    legend: {
      position: "top",
      labels: {
        font: {
          size: 14,
        },
        color: "#333",
      },
    },
    title: {
      display: true,
      text: "Overall Campaign Analysis",
      font: {
        size: 18,
        weight: "bold",
      },
      color: "#333",
    },
    tooltip: {
      enabled: true,
      callbacks: {
        label: (tooltipItem) => `Count: ${tooltipItem.raw}`,
      },
    },
    datalabels: {
      anchor: "end",
      align: "end",
      color: "#333",
      font: {
        size: 12,
        weight: "bold",
      },
      formatter: (value) => `${value}`,
    },
  },
  scales: {
    x: {
      title: {
        display: true,
        text: "Scale of Risk",
        font: {
          size: 14,
          weight: "bold",
        },
        color: "#84949A",
      },
      ticks: {
        font: {
          size: 12,
        },
        color: "#475657",
      },
    },
    y: {
      beginAtZero: true,
      title: {
        display: true,
        text: "Count",
        font: {
          size: 14,
          weight: "bold",
        },
        color: "#84949A",
      },
      ticks: {
        font: {
          size: 12,
        },
        color: "#475657",
      },
    },
  },
};
</script>

<style scoped>
.chart-container {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  height: 550px;
  margin: 0 auto;
}
</style>
