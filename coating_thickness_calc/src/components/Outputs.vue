<!-- Outputs.vue -->
<template>
    <div class="output_field">
      <div class="output_title">
        <p>Coating Thickness:</p>
      </div>
      <p>{{ calcCoatingThickness }}</p>
      <p>µm</p>
    </div>
  </template>
  
  <script setup>
  import { computed } from 'vue';
  
  // Accept the state object as a prop
  const props = defineProps({
    state: {
      type: Object,
      required: true
    }
  });
  
  // Computed property for coating thickness calculation
  const calcCoatingThickness = computed(() => {
    let ball_d = parseFloat(props.state.ball_d);
    let outer_d = parseFloat(props.state.outer_d);
    let inner_d = parseFloat(props.state.inner_d);
  
    if (isNaN(ball_d) || isNaN(outer_d) || isNaN(inner_d) || ball_d === 0) {
      return 'N/A';
    }
  
    let coating_thickness = (outer_d ** 2 - inner_d ** 2) / (4 * ball_d * 1000);
    return coating_thickness.toFixed(2);
  });
  </script>
  
  <style scoped>
  .output_field {
    display: flex;
    align-items: center;
    margin: 10px 0;
  }
  
  .output_title {
    width: 200px;
    font-weight: bold;
  }
  </style>