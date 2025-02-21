<template>
    <div>
      <label for="filters">Filter by:</label>
      <select id="filters" multiple v-model="selectedOptions" @change="emitFilterChange">
        <option value="alphabets">Alphabets</option>
        <option value="numbers">Numbers</option>
        <option value="highest_alphabet">Highest Alphabet</option>
      </select>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        selectedOptions: [],
      };
    },
    methods: {
      emitFilterChange() {
        this.$emit('filter-change', this.selectedOptions);
      },
    },
  };
  </script>
  
  <style scoped>
  select {
    width: 200px;
  }
  </style>
  