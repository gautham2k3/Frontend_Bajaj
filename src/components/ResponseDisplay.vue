<template>
    <div>
      <h2>Filtered Response</h2>
      <p v-if="selectedFilters.includes('alphabets')">
        <strong>Alphabets:</strong> {{ responseData.alphabets.join(', ') }}
      </p>
      <p v-if="selectedFilters.includes('numbers')">
        <strong>Numbers:</strong> {{ responseData.numbers.join(', ') }}
      </p>
      <p v-if="selectedFilters.includes('highest_alphabet')">
        <strong>Highest Alphabet:</strong> {{ responseData.highest_alphabet.join(', ') }}
      </p>
    </div>
  </template>
  
  <script>
  export default {
    props: ['responseData', 'selectedFilters'],
  };
  </script>
  
  <style scoped>
  h2 {
    margin-top: 20px;
  }
  </style>
  