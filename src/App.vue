<template>
  <div id="app">
    <div class="header">
      <div class="logo-container">
        <img src="https://upload.wikimedia.org/wikipedia/en/thumb/2/24/Seal_of_the_University_of_Santo_Tomas.svg/303px-Seal_of_the_University_of_Santo_Tomas.svg.png?20210111031237" class="logo" />
      </div>
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
  setup() {
    const weight = ref(null);
    const height = ref(null);
    const bmiResult = ref(null);

    const calculateBMI = () => {
      if (weight.value && height.value) {
        const heightInMeters = height.value / 100;
        bmiResult.value = weight.value / (heightInMeters * heightInMeters);
      } else {
        alert("Please enter weight and height.");
      }
    };

    const getBMICategory = (bmi) => {
      if (bmi < 18.5) {
        return "Underweight";
      } else if (bmi >= 18.5 && bmi < 24.9) {
        return "Normal weight";
      } else if (bmi >= 25 && bmi < 29.9) {
        return "Overweight";
      } else {
        return "Obese";
      }
    };

    return {
      weight,
      height,
      bmiResult,
      calculateBMI,
      getBMICategory,
    };
  },
};
</script>

<style>
body {
  background-color: #ffe600;
  background-size: cover;
  background-position: center;
  background-repeat: no-repeat;
  color: #090a0c;
  font-family: 'Arial', sans-serif;
  margin: 0;
  padding: 0;
}

.header {
  text-align: center;
  background-color: #d3a50c;
  color: #090a0c;
  padding: 5px;
  margin-bottom: 30px;
  display: flex;
  align-items: center;
  font-size: 2em;
}

.logo-container {
  margin-right: 10px;
}

.title {
  margin-bottom: 0;
}

.logo {
  max-width: 100px;
}

.calculator {
  border: 2px solid #090a0c;
  padding: 20px;
  border-radius: 8px;
  text-align: center;
  max-width: 400px;
  width: 80%;
  margin: 0 auto;
  background-color: #ffffff;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
}

.input-group {
  margin-bottom: 15px;
}

button {
  background-color: #090a0c;
  color: #c0c4b0;
  padding: 10px 20px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

button:hover {
  background-color: #001732;
}

.result {
  margin-top: 20px;
}

.category {
  color: #090a0c;
  font-weight: bold;
}

.bmi-chart {
  text-align: center;
  margin-top: 40px;
}

table {
  width: 100%;
  border-collapse: collapse;
  margin-top: 10px;
}

th, td {
  border: 1px solid #090a0c;
  padding: 15px;
  text-align: center;
}

th {
  background-color: #d3a50c;
  color: #090a0c;
  font-weight: bold;
}
</style>
