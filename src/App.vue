<template>
  <div>
    <label for="citySelect">Select a City:</label>
    <select id="citySelect" v-model="selectedCity">
      <option value="" disabled>Select a city</option>
      <option v-for="city in cityList" :key="city" :value="city">{{ city }}</option>
    </select>
    <p v-if="selectedCity">Selected City: {{ selectedCity }}</p>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';

const cityList = [
  'Holmdel, New Jersey',
  'Atlanta, Georgia',
  'San Francisco, California',
  'Basingstoke, United Kingdom',
  'London, Shoreditch, United Kingdom',
  'London, Canary Wharf, United Kingdom',
  'Tel Aviv-Yafo, Israel'
];

const selectedCity = ref('');
</script>

<style scoped>
#citySelect {
  margin: 10px;
  padding: 5px;
  font-size: 16px;
}
</style>
