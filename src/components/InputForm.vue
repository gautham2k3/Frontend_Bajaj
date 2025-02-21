<template>
    <form @submit.prevent="handleSubmit">
      <textarea 
        v-model="inputData"
        rows="5"
        cols="50"
        placeholder='Enter JSON here (e.g., {"data": ["A", "B", "1"]})'
      ></textarea>
      <button type="submit">Submit</button>
      <p v-if="error" style="color: red;">{{ error }}</p>
    </form>
  </template>
  
  <script>
  import axios from 'axios';
  
  export default {
    data() {
      return {
        inputData: '',
        error: '',
      };
    },
    methods: {
      async handleSubmit() {
        try {
          const parsedData = JSON.parse(this.inputData);
          const response = await axios.post('https://bajaj-backend-woad.vercel.app/bfhl', parsedData);
          this.$emit('api-response', response.data);
          this.error = '';
        } catch (err) {
          if (err instanceof SyntaxError) {
            this.error = 'Invalid JSON format.';
          } else {
            this.error = 'API error: ' + err.message;
          }
        }
      },
    },
  };
  </script>
