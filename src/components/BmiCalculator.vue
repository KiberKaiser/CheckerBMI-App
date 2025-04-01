<template>
  <div class="wrapper">
    <div class="content">
      <div class="calculator">
        <h1 class="title">BMI Calculator</h1>

        <div class="input-group">
          <label for="weight">Weight (kg):</label>
          <input v-model.number="weight" type="number" id="weight" />
        </div>

        <div class="input-group">
          <label for="height">Height (cm):</label>
          <input v-model.number="height" type="number" id="height" />
        </div>

        <div class="input-group">
          <label for="age">Age:</label>
          <input v-model.number="age" type="number" id="age" />
        </div>

        <button @click="calculateBMI">Calculate</button>

        <div v-if="bmi" class="result">
          <h2>Your BMI: {{ bmi }}</h2>
          <p :class="categoryClass">{{ category }}</p>
          <p class="age-category">{{ ageCategory }}</p>
        </div>

        <div class="bmi-table">
          <h2>BMI Categories</h2>
          <table>
            <thead>
            <tr>
              <th>BMI Range</th>
              <th>Category</th>
            </tr>
            </thead>
            <tbody>
            <tr class="underweight">
              <td>Less than 18.5</td>
              <td>Underweight</td>
            </tr>
            <tr class="normal">
              <td>18.5 - 24.9</td>
              <td>Normal weight</td>
            </tr>
            <tr class="overweight">
              <td>25 - 29.9</td>
              <td>Overweight</td>
            </tr>
            <tr class="obesity">
              <td>30 and above</td>
              <td>Obesity</td>
            </tr>
            </tbody>
          </table>
        </div>
      </div>

      <div class="info">
        <h2>What is BMI (Body Mass Index)?</h2>
        <p>
          BMI (Body Mass Index) is a numerical value derived from an individual's weight and height. It provides a general indication of whether a person has a healthy body weight for their height. Although BMI is not a perfect measurement, it is commonly used as a screening tool to assess whether a person is underweight, normal weight, overweight, or obese.
        </p>

        <h3>How is BMI Calculated?</h3>
        <p>
          BMI is calculated using the following formula:
        </p>
        <div class="formula">
          <p><strong>BMI = weight (kg) / [height (m)]²</strong></p>
        </div>

        <h4>Example:</h4>
        <p>
          If a person weighs <strong>70 kg</strong> and their height is <strong>1.75 meters</strong>, the BMI is calculated as:
        </p>
        <div class="example">
          <p><strong>BMI = 70 / (1.75 × 1.75) = 70 / 3.0625 ≈ 22.86</strong></p>
        </div>
        <h3>BMI Categories:</h3>
        <p>The BMI value helps categorize an individual's weight status into the following ranges:</p>
        <ul>
          <li><strong>Underweight:</strong> BMI &lt; 18.5 — This indicates that a person may be undernourished or at risk for malnutrition and should consult a healthcare provider to assess their health.</li>
          <li><strong>Normal weight:</strong> BMI 18.5 - 24.9 — This is considered a healthy weight range for most adults and is associated with lower risks for chronic diseases.</li>
          <li><strong>Overweight:</strong> BMI 25 - 29.9 — People with a BMI in this range may have an increased risk of health issues such as diabetes and heart disease.</li>
          <li><strong>Obesity:</strong> BMI ≥ 30 — Obesity is associated with a higher risk of serious health conditions like cardiovascular diseases, type 2 diabetes, and certain types of cancer.</li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script setup>
import {ref, computed} from 'vue';

const weight = ref(null);
const height = ref(null);
const age = ref(null);
const bmi = ref(null);

const category = computed(() => {
  if (!bmi.value) return '';
  if (bmi.value < 18.5) return 'Underweight';
  if (bmi.value >= 18.5 && bmi.value < 24.9) return 'Normal weight';
  if (bmi.value >= 25 && bmi.value < 29.9) return 'Overweight';
  return 'Obesity';
});

const categoryClass = computed(() => {
  if (!bmi.value) return '';
  if (bmi.value < 18.5) return 'underweight';
  if (bmi.value >= 18.5 && bmi.value < 24.9) return 'normal';
  if (bmi.value >= 25 && bmi.value < 29.9) return 'overweight';
  return 'obesity';
});

const ageCategory = computed(() => {
  if (!age.value) return '';
  if (age.value < 18) return 'Youth BMI ranges may differ';
  if (age.value >= 18 && age.value < 65) return 'Adult BMI standard applies';
  return 'Elderly individuals may have different BMI ranges';
});

const calculateBMI = () => {
  if (weight.value && height.value) {
    let heightInMeters = height.value / 100;
    bmi.value = (weight.value / (heightInMeters * heightInMeters)).toFixed(2);
  }
};
</script>

<style scoped>

.wrapper {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 94vh;
  background: linear-gradient(to right, #00c6ff, #0072ff);
  padding: 20px;
}

.content {
  font-family: "Segoe UI";
  display: flex;
  max-width: 1200px;
  width: 100%;
  gap: 20px;
  justify-content: space-between;
}

.calculator {
  flex: 1 1 40%;
  background: white;
  padding: 20px;
  border-radius: 12px;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
  text-align: center;
  height: 100%;
  min-height: 500px;
}

.input-group {
  margin: 10px 0;
  text-align: left;
}

label {
  font-family: "Segoe UI";
  font-weight: bold;
  display: block;
}

input {
  width: 100%;
  padding: 10px;
  margin-top: 5px;
  border-radius: 5px;
  border: 1px solid #ccc;
  box-sizing: border-box;
}

button {
  width: 100%;
  padding: 12px;
  background: #007bff;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  font-size: 16px;
  margin-top: 10px;
}

button:hover {
  background: #0056b3;
}

.bmi-table {
  margin-top: 20px;
  width: 100%;
}

table {
  width: 100%;
  table-layout: fixed;
  border-collapse: collapse;
}

th, td {
  font-family: "Segoe UI";
  padding: 10px;
  text-align: center;
  word-wrap: break-word;
}

th {

  background: #ddd;
}

.underweight {
  background: #add8e6;
}

.normal {
  background: #90ee90;
}

.overweight {
  background: #ffd700;
}

.obesity {
  background: #ff6347;
}

.info {
  font-family: "Segoe UI";
  flex: 1 1 60%;
  background: #f9f9f9;
  padding: 20px;
  border-radius: 12px;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
  text-align: left;
}

@media (max-width: 768px) {
  .content {
    flex-direction: column;
  }
}
</style>
