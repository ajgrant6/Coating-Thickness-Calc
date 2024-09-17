<template>
  <div class="output_field">
    <div class="output_title">
      <p>Coating Thickness:</p>
    </div>
    <p>{{ calcCoatingThickness }}</p>
    <p>µm</p>
  </div>

  <!-- New Output for Diameter Ratio -->
  <div class="output_field">
    <div class="output_title">
      <p>Diameter Ratio:</p>
    </div>
    <p>{{ calcDiameterRatio }}%</p>
    <p :class="ratioStatusClass">{{ ratioStatus }}</p> <!-- Add status label -->
  </div>
</template>

<script setup>
import { computed } from 'vue';

// Accept the state object as a prop
const props = defineProps({
  state: {
    type: Object,
    required: true,
  },
});

// Computed property for coating thickness calculation
const calcCoatingThickness = computed(() => {
  const ball_d = parseFloat(props.state.ball_d);
  const outer_d = parseFloat(props.state.outer_d);
  const inner_d = parseFloat(props.state.inner_d);

  if (isNaN(ball_d) || isNaN(outer_d) || isNaN(inner_d) || ball_d === 0) {
    return 'N/A';
  }

  const coating_thickness = (outer_d ** 2 - inner_d ** 2) / (4 * ball_d * 1000);
  return coating_thickness.toFixed(2);
});

// New computed property for the Diameter Ratio
const calcDiameterRatio = computed(() => {
  const outer_d = parseFloat(props.state.outer_d);
  const inner_d = parseFloat(props.state.inner_d);

  if (isNaN(outer_d) || isNaN(inner_d) || inner_d <= 0) {
    return '0'; // If inner diameter is less than or equal to 0, return 0
  }

  const diameter_ratio = (inner_d / outer_d) * 100; // Get ratio as a percentage
  return diameter_ratio.toFixed(2); // Returns the result rounded to 2 decimal places
});

// Computed property to determine the status of the ratio
const ratioStatus = computed(() => {
  const ratio = parseFloat(calcDiameterRatio.value);

  if (ratio >= 40 && ratio <= 60) {
    return 'Good';
  } else if (ratio >= 30 && ratio <= 70) {
    return 'OK';
  } else {
    return 'Bad';
  }
});

// Add a class for visual indication based on the ratio status
const ratioStatusClass = computed(() => {
  const ratio = ratioStatus.value;
  
  if (ratio === 'Good') {
    return 'status-good';
  } else if (ratio === 'OK') {
    return 'status-ok';
  } else {
    return 'status-bad';
  }
});
</script>

<style scoped>
.output_field {
  display: flex;
  align-items: center;
  margin: 10px 0;
}

.output_title {
  flex: 1;
  font-weight: bold;
}

.output_field p {
  margin-left: 10px;
}

/* Styles to signal the ratio status */
.status-good {
  color: green;
  font-weight: bold;
}

.status-ok {
  color: orange;
  font-weight: bold;
}

.status-bad {
  color: red;
  font-weight: bold;
}
</style>