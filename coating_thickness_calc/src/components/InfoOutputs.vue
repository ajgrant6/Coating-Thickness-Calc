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
    <p>{{ calcDiameterRatio }}</p>
    <p>%</p>
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

  const diameter_ratio = inner_d / outer_d;
  return (diameter_ratio*100).toFixed(0); // Returns the result rounded to 2 decimal places
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
</style>