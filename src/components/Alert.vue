<template>
<div class="alert-container">
    <v-data-table
    :items="items"
    :headers="headers"
    class="elevation-1"
    :items-per-page="10"
    >
    <template #[`item.action`]="{ item }">
        <v-btn  @click="downloadReport(item)">
        {{ item.action }}
        </v-btn>
    </template>
    </v-data-table>
</div>
</template>

<script setup>
import { defineProps } from "vue";

const props = defineProps({
items: {
    type: Array,
    default: () => [],
},
});

// console.log("Alert.vue : props.items", props.items);

// Define headers for the v-data-table
const headers = [
    { title: "ID", value: "id" },
    { title: "Name", value: "name" },
    { title: "Date", value: "date" },
    { title: "High", value: "high" },
    { title: "Medium", value: "medium" },
    { title: "Low", value: "low" },
    { title: "action", value: "action" },
];


function jsonToCsv(data) {
    const csvRows = [];
    const headers = Object.keys(data[0]);
    csvRows.push(headers.join(',')); 
    for (const row of data) {
        const values = headers.map(header => JSON.stringify(row[header] ?? "")); // Convert values to strings and handle null/undefined
        csvRows.push(values.join(','));
    }
    return csvRows.join('\n');
}


function downloadReport(item) {
    const itemDownloadReport = item.downloadReport;
    const csvData = jsonToCsv(itemDownloadReport);
    const blob = new Blob([csvData], { type: "text/csv" });
    const link = document.createElement("a");
    const fileName = item.name ? `${item.name} report.csv` : "default_report.csv";

    // Trigger CSV file download
    link.href = URL.createObjectURL(blob);
    link.download = fileName;
    document.body.appendChild(link);
    link.click();
    document.body.removeChild(link);
}




</script>

<style scoped>
.alert-container {
padding: 1rem;
}
</style>
