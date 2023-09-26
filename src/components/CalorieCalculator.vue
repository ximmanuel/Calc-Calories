<template>
    <main class="container text-light rounded p-4">
        <h1 class="mb-4">Calc-Calories</h1>

        <div class="row">
            <div class="col-sm-6">
                <div class="form-group">
                    <label for="genderSelect">Gender: </label>
                    <select id="genderSelect" v-model="gender" class="form-control">
                        <option value="male">Male</option>
                        <option value="female">Female</option>
                    </select>
                </div>

                <div class="form-group">
                    <label for="heightInput">Height (cm): </label>
                    <input id="heightInput" type="number" v-model="height" class="form-control">
                </div>

                <div class="form-group">
                    <label for="weightInput">Weight (kg): </label>
                    <input id="weightInput" type="number" v-model="weight" class="form-control">
                </div>

                <div class="form-group">
                    <label for="ageInput">Age: </label>
                    <input id="ageInput" type="number" v-model="age" class="form-control">
                </div>

                <div class="form-group">
                    <label for="bodyFatInput">Body Fat Percentage (%): </label>
                    <input id="bodyFatInput" type="number" v-model="bodyFatPercentage" class="form-control">
                </div>
            </div>

            <div class="col-sm-6">
                <div class="mt-4">
                    <strong>Individual Results:</strong>
                    <ul class="list-group">
                        <li v-for="(cal, index) in calories" :key="index" class="list-group-item">
                            {{ formulaNames[index] }}: {{ cal.toFixed(2) }}
                        </li>
                    </ul>
                </div>

                <p class="mt-3">
                    Average Calories: {{ averageCalories }}
                </p>

                <button @click="calculateCalories" class="btn btn-primary mt-3">
                    Calculate Calories
                </button>
            </div>
        </div>

        <footer class="mt-5">
            <small>Made by LYTEX MEDIA</small>
        </footer>
    </main>
</template>

<style lang="scss" scoped>
  @import '../assets/scss/styles.scss';
</style>

<script>
export default {
  data() {
    return {
      gender: "male",
      height: null,
      weight: null,
      age: null,
      bodyFatPercentage: 25,
      calories: [],
      formulaNames: ["Harris-Benedict", "Mifflin-St Jeor", "Katch-McArdle"]
    };
  },
  computed: {
    averageCalories() {
      return this.calories.length > 0 ? (this.calories.reduce((a, b) => a + b, 0) / this.calories.length).toFixed(2) : 0;
    },
  },
  methods: {
    calculateCalories() {
      this.calories = [
        this.calculateHarrisBenedict(),
        this.calculateMifflinStJeor(),
        this.calculateKatchMcArdle()
      ];
    },
    calculateHarrisBenedict() {
      return this.gender === "male"
        ? 88.362 + (13.397 * this.weight) + (4.799 * this.height) - (5.677 * this.age)
        : 447.593 + (9.247 * this.weight) + (3.098 * this.height) - (4.330 * this.age);
    },
    calculateMifflinStJeor() {
      return this.gender === "male"
        ? 10 * this.weight + 6.25 * this.height - 5 * this.age + 5
        : 10 * this.weight + 6.25 * this.height - 5 * this.age - 161;
    },
    calculateKatchMcArdle() {
      let leanBodyMass = this.weight - (this.weight * this.bodyFatPercentage * 0.01);
      return 370 + (21.6 * leanBodyMass);
    }
  },
};
</script>
