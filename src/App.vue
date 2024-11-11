<script setup>
import Navbar from "@/components/Navbar.vue";
import Filters from "@/components/Filters.vue";
import { RouterLink, RouterView } from "vue-router";
</script>

<template>
  <Navbar />
  <Filters />
  <RouterView />
</template>
