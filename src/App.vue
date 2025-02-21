<script setup>
import { ref } from 'vue';
import InputForm from "@/components/InputForm.vue";
import MultiSelectDropdown from "@/components/MultiSelectDropdown.vue";
import ResponseDisplay from "@/components/ResponseDisplay.vue";

const responseData = ref(null);
const selectedFilters = ref([]);

function handleApiResponse(data) {
  responseData.value = data;
}

function handleFilterChange(filters) {
  selectedFilters.value = filters;
}
</script>

<template>
  <div class="home-page">
    <h1>Welcome to the Bajaj Finserv Health Dev Challenge</h1>
    <InputForm @api-response="handleApiResponse" />
    <MultiSelectDropdown v-if="responseData" @filter-change="handleFilterChange" />
    <ResponseDisplay v-if="responseData" :response-data="responseData" :selected-filters="selectedFilters" />
  </div>
</template>

<style scoped>
header {
  line-height: 1.5;
}
.home-page {
  text-align: center;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
