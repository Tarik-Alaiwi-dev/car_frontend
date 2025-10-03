<template>
  <div id="app">
    <PredictForm />
  </div>
</template>

<script>
import PredictForm from "./components/PredictForm.vue";

export default {
  name: "App",
  components: { PredictForm },
};
</script>

<style>
#app {
  text-align: center;
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>
