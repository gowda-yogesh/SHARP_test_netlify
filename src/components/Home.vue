<template>
  <section class="pr-10 pl-10 mb-4">
    <div v-if="barChartData">
      <BarChart :barChartData="barChartData" />
    </div>
    <div v-else class="d-flex justify-center">
      <v-progress-circular
        indeterminate
        color="#FF5C8D"
        size="50"
      ></v-progress-circular>
    </div>
  </section>
</template>

<script setup>
import { ref, defineProps, onMounted,  } from "vue";
import BarChart from "@/components/BarChart.vue";
import axios from 'axios';

const finalResult = ref(null);
const barChartData = ref(null);


onMounted(async () => {
  try {
    // Demo Code 
    const localData = await axios.get('/final_limit_150_results_json.json');
    // await new Promise(resolve => setTimeout(resolve, 4500));
    finalResult.value = localData.data;
    console.log("Home.vue : onMounted : localData", localData.data);

    // //Actual Code
    // const response = await axios.get('http://localhost:8000/api/simple_get_api/')
    // finalResult.value = response.data;
    // console.log("Home.vue : onMounted", response.data)
    
    barChartData.value = finalResult.value?.final_result?.overall_analysis || null;
  } catch (error) {
    console.error('Error fetching data:', error)
  } finally {
    console.log('Request completed')  // This will run regardless of success or error
  }
})





</script>