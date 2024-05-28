<template>
  <div>
    <label>Select a City:</label>
    <div
        v-for="city in cityList"
        :key="city"
        @click="selectCity(city)"
        class="city-item"
    >
      {{ city }}
    </div>
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

const selectCity = (city: string) => {
  selectedCity.value = city;
};
</script>

<style scoped>
.city-item {
  width: 400px;
  margin: 10px 0;
  padding: 10px;
  border: 1px solid #ccc;
  cursor: pointer;
}
.city-item:hover {
  background-color: #f0f0f0;
}
</style>
