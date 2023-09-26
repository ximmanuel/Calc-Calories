<template>
  <div id="app">
    <CalorieCalculator />
  </div>
</template>

<script>
import CalorieCalculator from "./components/CalorieCalculator.vue";

export default {
  components: {
    CalorieCalculator
  }
};
</script>

<style>
#app {
  text-align: center;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  background-color: #212529;
  height: 100vh;
}
</style>
