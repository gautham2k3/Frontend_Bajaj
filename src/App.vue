<template>
  <div>
    <h2>API Request & Response</h2>
    <form @submit.prevent="handleSubmit">
      <textarea 
        v-model="inputData"
        rows="5"
        cols="50"
        placeholder='Enter JSON here (e.g., {"data": ["A", "B", "1"]})'
      ></textarea>
      <br />
      
      <div class="dropdown-container">
        <label>Select Response Fields(Hold Shift to select multiple):</label>
        <select v-model="selectedFields" multiple>
          <option value="alphabets">Alphabets</option>
          <option value="numbers">Numbers</option>
          <option value="highest_alphabet">Highest Alphabet</option>
        </select>
      </div>

      <button type="submit">Submit</button>
      <p v-if="error" style="color: red;">{{ error }}</p>
    </form>
    
    <div v-if="responseData">
      <h3>Filtered Response:</h3>
      <div class="response-container">
        <div v-if="selectedFields.includes('alphabets') && responseData.alphabets?.length" class="response-card">
          <h4>Alphabets</h4>
          <p>{{ responseData.alphabets.join(', ') }}</p>
        </div>
        <div v-if="selectedFields.includes('numbers') && responseData.numbers?.length" class="response-card">
          <h4>Numbers</h4>
          <p>{{ responseData.numbers.join(', ') }}</p>
        </div>
        <div v-if="selectedFields.includes('highest_alphabet') && responseData.highest_alphabet" class="response-card">
          <h4>Highest Alphabet</h4>
          <p>{{ responseData.highest_alphabet }}</p>
        </div>
      </div>
    </div>
  </div>
</template>




<script>
import axios from 'axios';

export default {
  data() {
    return {
      inputData: '',
      responseData: null,
      error: '',
      selectedFields: [] 
    };
  },
  methods: {
    async handleSubmit() {
      this.error = '';
      this.responseData = null;
      
      if (!this.inputData.trim()) {
        this.error = 'Input cannot be empty.';
        return;
      }
      
      try {
        const parsedData = JSON.parse(this.inputData);
        if (!parsedData.data || !Array.isArray(parsedData.data)) {
          this.error = 'Invalid JSON format: Expecting { "data": [...] }';
          return;
        }
        
        const response = await axios.post('https://bajaj-backend-woad.vercel.app/bfhl', parsedData);
        this.responseData = response.data;
      } catch (err) {
        this.error = err instanceof SyntaxError 
          ? 'Invalid JSON format.'
          : 'API error: ' + err.message;
      }
    }
  }
};
</script>



<style scoped>
/* General styling */
div {
  max-width: 600px;
  margin: auto;
  text-align: center;
}
textarea {
  width: 100%;
  margin-bottom: 15px;
}
button {
  margin-top: 10px;
}
.dropdown-container {
  margin: 15px 0;
  text-align: left;
}
select {
  width: 100%;
  padding: 8px;
  margin-top: 5px;
}
select[multiple] {
  height: 100px;
}

/* Styling for the filtered response */
.response-container {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-around;
  gap: 20px;
  margin-top: 20px;
}
.response-card {
  background-color: #f9f9f9;
  border-radius: 8px;
  box-shadow: 0px 4px 6px rgba(0,0,0,0.1);
  padding: 15px;
  color: black;
  width: calc(50% - 20px); /* Adjust width for responsive layout */
}
.response-card h4 {
  margin-bottom: 10px;
}
.response-card p {
  margin: 0;
}
</style>
