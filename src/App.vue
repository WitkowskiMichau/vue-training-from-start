<template>
  <div>
    <label for="citySelect">Select a City:</label>
    <select id="citySelect">
      <option v-for="city in cityList" :key="city">{{ city }}</option>
    </select>
  </div>
</template>

<script setup lang="ts">
const cityList = [
  'Holmdel, New Jersey',
  'Atlanta, Georgia',
  'San Francisco, California',
  'Basingstoke, United Kingdom',
  'London, Shoreditch, United Kingadom',
  'London, Canary Wharf, United Kingdom',
  'Tel Aviv-Yafo, Israel'
];
</script>

<style scoped>
#citySelect {
  margin: 10px;
  padding: 5px;
  font-size: 16px;
}
</style>
