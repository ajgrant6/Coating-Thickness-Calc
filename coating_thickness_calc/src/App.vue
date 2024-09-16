<!-- App.vue -->
<script setup>
import { reactive } from 'vue';
import Inputs from './components/Inputs.vue';
import Outputs from './components/Outputs.vue';
import Visualization from './components/Visualization.vue';

// Central state
const state = reactive({
  ball_d: '',
  outer_d: '',
  inner_d: '',
});
</script>

<template>
  <header></header>

  <main>
    <div>
      <Inputs :state="state" />
      <Outputs :state="state" />
    </div>
    <Visualization :state="state" />
  </main>
</template>

<style scoped>
/* Styles can go here */
</style>