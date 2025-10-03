<template>
  <div class="form-container">
    <h2>Car Price Prediction</h2>
    <form @submit.prevent="submitForm">
      <label>Levy</label>
      <input v-model="form.levy" type="number" step="1" required />

      <label>Production Year</label>
      <input v-model="form.prod_year" type="number" required />

      <label>Mileage</label>
      <input v-model="form.mileage" type="number" step="1" required />

      <label>Engine Volume</label>
      <input v-model="form.engine_volume" type="number" step="0.1" required />

      <label>Cylinders</label>
      <input v-model="form.cylinders" type="number" required />

      <label>Model Name</label>
      <input v-model="form.model" type="text" required />

      <button type="submit">Predict</button>
    </form>

    <div v-if="result" class="result">
      <h3>Result:</h3>
      <pre>{{ result }}</pre>
    </div>
  </div>
</template>

<script>
export default {
  name: "PredictForm",
  data() {
    return {
      form: {
        levy: "100",
        prod_year: "2018",
        mileage: "120000",
        engine_volume: "2.0",
        cylinders: "4",
        model: "Prius",
      },
      result: null,
    };
  },
  methods: {
    async submitForm() {
      try {
        const response = await fetch("https://web-production-045c3.up.railway.app/api/predict/", {
          method: "POST",
          headers: { "Content-Type": "application/json" },
          body: JSON.stringify(this.form),
        });
        this.result = await response.json();
      } catch (error) {
        console.error("Error:", error);
      }
    },
  },
};
</script>

<style scoped>
.form-container {
  max-width: 400px;
  margin: 20px auto;
  padding: 15px;
  border: 1px solid #ccc;
  border-radius: 8px;
  font-family: sans-serif;
}
form {
  display: flex;
  flex-direction: column;
}
label {
  margin-top: 10px;
  font-weight: bold;
}
input {
  padding: 6px;
  margin-top: 4px;
  border: 1px solid #aaa;
  border-radius: 4px;
}
button {
  margin-top: 15px;
  padding: 10px;
  border: none;
  border-radius: 6px;
  background: #4caf50;
  color: white;
  cursor: pointer;
}
button:hover {
  background: #45a049;
}
.result {
  margin-top: 20px;
  padding: 10px;
  border: 1px solid #eee;
  background: #f9f9f9;
  color: black;
}
</style>
