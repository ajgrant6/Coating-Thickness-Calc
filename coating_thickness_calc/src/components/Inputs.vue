<!-- Inputs.vue -->
<template>
    <div>
      <div class="input_field">
        <div class="input_title">
          <p>Ball Diameter:</p>
        </div>
        <input type="text" v-model="state.ball_d" placeholder="30">
        <p>mm</p>
      </div>
      <div class="input_field">
        <div class="input_title">
          <p>Outer Crater Diameter:</p>
        </div>
        <input type="text" v-model="state.outer_d" placeholder="470">
        <p>µm</p>
      </div>
      <div class="input_field">
        <div class="input_title">
          <p>Inner Crater Diameter:</p>
        </div>
        <input type="text" v-model="state.inner_d" placeholder="240">
        <p>µm</p>
      </div>
    </div>
  </template>
  
  <script setup>
  // Accept the state object as a prop
  const props = defineProps({
    state: {
      type: Object,
      required: true
    }
  });
  </script>
  
  <style scoped>
  .input_field {
    display: flex;
    align-items: center;
    margin: 10px 0;
  }
  
  .input_title {
    width: 200px;
    font-weight: bold;
  }
  </style>