<script setup>
import { RouterLink, useRoute } from 'vue-router';
import BL_primary_icon from '@/assets/img/23_BL_primary_icon.svg';

const isActiveLink = (routePath) => {
  const route = useRoute();
  return route.path === routePath;
};
</script>

<template>
  <nav class="bg-[#FFDD33] border-b border-yellow-900">
    <div class="mx-auto max-w-7xl px-2 sm:px-6 lg:px-8">
      <div class="flex h-20 items-center justify-between">
        <div
          class="flex flex-1 items-center justify-center md:items-stretch md:justify-start"
        >
          <!-- bl_logo -->
          <RouterLink class="flex flex-shrink-0 items-center mr-4" to="/">
            <img class="h-10 w-auto" :src="BL_primary_icon" alt="Vue Jobs" />
            <span class="hidden md:block text-white text-2xl font-bold ml-2"
              >SHARP</span
            >
          </RouterLink>
          <div class="md:ml-auto">
            <div class="flex space-x-2">
              <RouterLink
                to="/"
                :class="[
                  isActiveLink('/')
                    ? 'bg-yellow-500'
                    : 'hover:bg-yellow-400 hover:text-white',
                  'text-white',
                  'px-3',
                  'py-2',
                  'rounded-md',
                  'font-bold'
                ]"
                >Home</RouterLink
              >
              <RouterLink
                to="/alerts"
                :class="[
                  isActiveLink('/alerts')
                    ? 'bg-yellow-500'
                    : 'hover:bg-yellow-400 hover:text-white',
                  'text-white',
                  'px-3',
                  'py-2',
                  'rounded-md',
                  'font-bold'
                ]"
                >Alerts</RouterLink
              >
              <RouterLink
                to="/connect"
                :class="[
                  isActiveLink('/connect')
                    ? 'bg-yellow-500'
                    : 'hover:bg-yellow-400 hover:text-white',
                  'text-white',
                  'px-3',
                  'py-2',
                  'rounded-md',
                  'font-bold'
                ]"
                >Connect</RouterLink
              >
            </div>
          </div>
        </div>
      </div>
    </div>
  </nav>
</template>
