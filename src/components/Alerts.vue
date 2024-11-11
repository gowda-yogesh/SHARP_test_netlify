<template>
  <section class="pr-10 pl-10 mb-4">
    <div v-if="items">
      <div>
        <v-row class="mb-4" align="center" justify="space-around">
        <v-col cols="12" sm="4">
          <v-card color="#BA3030">
            <v-card-title class="text-h5">High Alerts</v-card-title>
            <v-card-text>
              <p>Count: {{overall_analysis.high}}</p>
              <p>Additional Details: Download Report ASAP and make necessary fix </p>
            </v-card-text>
          </v-card>
        </v-col>

        <v-col cols="12" sm="4">
          <v-card color="#FBA04B">
            <v-card-title class="text-h5">Medium Alerts</v-card-title>
            <v-card-text>
              <p>Count: {{overall_analysis.medium}}</p>
              <p>Additional Details: Try to fix this issue soon</p>
            </v-card-text>
          </v-card>
        </v-col>

        <v-col cols="12" sm="4">
          <v-card color="#FFDD33">
            <v-card-title class="text-h5">Low Alerts</v-card-title>
            <v-card-text>
              <p>Count:{{overall_analysis.low}} </p>
              <p>Additional Details: Have time to fix these issues</p>
            </v-card-text>
          </v-card>
        </v-col>
        </v-row>
      </div>
      
      <Alert :items="items" />
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
import { ref, onMounted } from "vue";
import axios from "axios";
import Alert from "./Alert.vue"; // Adjust the path as needed

const items = ref(null);
const overall_analysis = ref(null);

onMounted(async () => {
  try {
    // const response = await axios.get("http://localhost:8000/api/simple_get_api/");
    const localData = await axios.get('/final_limit_150_results_json.json');
    // await new Promise(resolve => setTimeout(resolve, 4500));
    console.log("Alert.vue : onMounted : localData", localData.data);
    const response = localData;
    overall_analysis.value = response.data?.final_result?.overall_analysis; 
    const individualAnalyses = response.data?.final_result?.individual_analyses; 

    // Map individual analyses data to match the table structure
    items.value = individualAnalyses.map((analysis, index) => ({
      id: index + 1, // Auto-incremented ID
      name: analysis.analysis_name,
      date: new Date().toLocaleDateString(), // Current date
      high: analysis.graph_analysis.high,
      medium: analysis.graph_analysis.medium,
      low: analysis.graph_analysis.low,
      action: "Download" ,// Placeholder text for the action column
      downloadReport: analysis.full_analysis// Placeholder text for the action column
    }));

  } catch (error) {
    console.error("Error fetching data:", error);
  }
});
</script>
