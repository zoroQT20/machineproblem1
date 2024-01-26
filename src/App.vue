<template>
  <div id="app">
    <div class="header">
      <h4 class="title">UST BMI Calculator</h4>
    </div>

    <div class="calculator">
      <h5>BMI Calculator</h5>
      <div class="input-group">
        <label for="weight">Weight (kg): </label>
        <input type="number" v-model="weight" id="weight" placeholder="Enter weight" />
      </div>
      <div class="input-group">
        <label for="height">Height (cm): </label>
        <input type="number" v-model="height" id="height" placeholder="Enter height" />
      </div>
      <button class="calculate-button" @click="calculateBMI">Calculate BMI</button>

      <div v-if="bmiResult !== null" class="result">
        <h6>Your BMI: {{ bmiResult.toFixed(2) }}</h6>
        <div class="category">{{ getBMICategory(bmiResult) }}</div>
      </div>
    </div>

    <div class="bmi-chart">
      <h5>BMI Categories</h5>
      <table>
        <thead>
          <tr>
            <th>Category</th>
            <th>Range</th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <td>Underweight</td>
            <td>&lt; 18.5</td>
          </tr>
          <tr>
            <td>Normal weight</td>
            <td>18.5 - 24.9</td>
          </tr>
          <tr>
            <td>Overweight</td>
            <td>25 - 29.9</td>
          </tr>
          <tr>
            <td>Obese</td>
            <td>&ge; 30</td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
import { ref } from 'vue';

export default {
  data() {
    return {
      weight: null,
      height: null,
      bmiResult: null,
    };
  },
  methods: {
    calculateBMI() {
      if (this.weight && this.height) {
        const heightInMeters = this.height / 100;
        this.bmiResult = this.weight / (heightInMeters * heightInMeters);
      } else {
        alert("Please enter weight and height.");
      }
    },
    getBMICategory(bmi) {
      if (bmi < 18.5) {
        return "Underweight";
      } else if (bmi >= 18.5 && bmi < 24.9) {
        return "Normal weight";
      } else if (bmi >= 25 && bmi < 29.9) {
        return "Overweight";
      } else {
        return "Obese";
      }
    },
  },
};
</script>

<style>
/* Your styles remain unchanged */
</style>

<style>
body {
  background-color: #ffe600; /* UST Gold */
  color: #00205b; /* UST Blue text color */
  font-family: 'Arial', sans-serif; /* Font family for better visibility */
  margin: 0;
  padding: 0;
}

.header {
  text-align: center;
  background-color: #00205b; /* UST Blue */
  color: #ffffff;
  padding: 20px;
  margin-bottom: 20px;
}

.title {
  margin-bottom: 0;
}

.calculator {
  border: 2px solid #00205b; /* UST Blue */
  padding: 20px;
  border-radius: 8px;
  text-align: center;
  max-width: 400px;
  width: 80%;
  margin: 0 auto;
  background-color: #ffffff; /* White background color for the calculator */
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
}

.input-group {
  margin-bottom: 15px;
}

button {
  background-color: #00205b; /* UST Blue */
  color: #ffffff;
  padding: 10px 20px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

button:hover {
  background-color: #001732; /* Darker shade of UST Blue */
}

.result {
  margin-top: 20px;
}

.category {
  color: #00205b; /* UST Blue */
  font-weight: bold;
}

.bmi-chart {
  text-align: center;
  margin-top: 40px;
}

/* Table styles */
table {
  width: 100%;
  border-collapse: collapse;
  margin-top: 10px;
}

th, td {
  border: 1px solid #00205b; /* UST Blue */
  padding: 10px;
  text-align: center;
}

th {
  background-color: #00205b; /* UST Blue */
  color: #ffffff;
}
</style>
