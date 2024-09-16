<template>
    <div class="visualization">
      <svg :width="size" :height="size" viewBox="0 0 200 200">
        <!-- Background Circle (Gray) -->
        <circle
          v-if="!hasValidInputs"
          cx="100"
          cy="100"
          r="80"
          fill="gray"
        />
        <!-- Outer Crater Circle (Orange Donut Shape) -->
        <g v-else>
          <!-- Outer Circle -->
          <circle
            :r="outerRadius"
            cx="100"
            cy="100"
            fill="orange"
          />
          <!-- Inner Circle (Cutout) -->
          <circle
            :r="innerRadius"
            cx="100"
            cy="100"
            fill="white"
          />
        </g>
      </svg>
    </div>
  </template>
  
  <script setup>
  import { computed } from 'vue';
  
  // Accept the shared state as a prop
  const props = defineProps({
    state: {
      type: Object,
      required: true,
    },
  });
  
  // Computed properties for validation
  const hasValidInputs = computed(() => {
    const outerD = parseFloat(props.state.outer_d);
    const innerD = parseFloat(props.state.inner_d);
    return (
      !isNaN(outerD) &&
      !isNaN(innerD) &&
      outerD > innerD &&
      outerD > 0 &&
      innerD >= 0
    );
  });
  
  // Define the size of the SVG canvas
  const size = 200;
  
  // Scale factors to fit the circles within the SVG viewBox
  const maxDiameter = 160; // Maximum diameter that fits in the SVG
  const scaleFactor = computed(() => {
    const outerD = parseFloat(props.state.outer_d) || 1;
    return maxDiameter / outerD;
  });
  
  // Computed radii for the circles
  const outerRadius = computed(() => {
    const outerD = parseFloat(props.state.outer_d);
    return ((outerD * scaleFactor.value) / 2) || 0;
  });
  
  const innerRadius = computed(() => {
    const innerD = parseFloat(props.state.inner_d);
    return ((innerD * scaleFactor.value) / 2) || 0;
  });
  </script>
  
  <style scoped>
  .visualization {
    margin: 20px 0;
  }
  </style>