<template>
  <div class="select-container">
    <v-select
      label="Account"
      :items="['6955199953']"
      variant="solo-filled"
      v-model="selectedAccount"  
    ></v-select>
    <v-select
      label="Campaign"
      :items="['All Campaigns']"
      variant="solo-filled"
      v-model="selectedCampaign" 
    ></v-select>
    <v-select
      label="Ads"
      :items="['All Ads']"
      variant="solo-filled"
      v-model="selectedAds" 
    ></v-select>
    <v-select
      label="Platform"
      :items="['Google Search']"
      variant="solo-filled"
      v-model="selectedPlatform" 
    ></v-select>
  </div>
</template>

<script setup>
import { ref } from 'vue';
const selectedAccount = ref('6955199953'); 
const selectedCampaign = ref('All Campaigns');
const selectedAds = ref('All Ads');
const selectedPlatform = ref('Google Search');
</script>

<style scoped>
.select-container {
  margin: 2rem 2rem;
  padding: 0rem 1rem ;
  display: flex;
  justify-content: space-between; /* Distributes the space evenly */
  gap: 16px; /* Optional: Adds some spacing between each select */
}

v-select {
  flex: 1; /* Makes each select take equal width */
}
</style>
