<!-- App.vue -->
<script setup>
import { reactive } from 'vue';
import InfoInputs from './components/InfoInputs.vue';
import InfoOutputs from './components/InfoOutputs.vue';
import CraterVisualization from './components/CraterVisualization.vue';

// Central state
const state = reactive({
  ball_d: '',
  outer_d: '',
  inner_d: '',
});
</script>

<template>
  <main>
    <div class="info">
      <div class="text_info">
        <InfoInputs :state="state" />
        <InfoOutputs :state="state" />
      </div>
      <div class="visual_info">
        <CraterVisualization :state="state" />
      </div>
    </div>
  </main>
</template>

<style scoped>
/* Container styling */
.info {
  display: flex;
  flex-wrap: wrap;             /* Allows items to wrap on smaller screens */
  justify-content: center;     /* Centers items horizontally */
  align-items: flex-start;     /* Aligns items to the top */
  max-width: 1200px;           /* Optional: limits container width */
  margin: 0 auto;              /* Centers the container within the page */
  width: 100%;
}

/* Flex items with fixed width */
.text_info,
.visual_info {
  flex: 0 0 300px;             /* Fixed width of 500px for both sections */
  box-sizing: border-box;
  margin: 10px;
  width: 500px;                /* Enforces the fixed width */
}
</style>