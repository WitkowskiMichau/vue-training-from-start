<template>
  <div>
    <label>Select a City:</label>
    <div
        v-for="city in cityList"
        :key="city"
        @click="selectCity(city)"
        @mouseenter="onHover(city)"
        @mouseleave="onLeave"
        :class="{'hovered': hoveredCity === city}"
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
const hoveredCity = ref('');

const selectCity = (city: string) => {
  selectedCity.value = city;
};

const onHover = (city: string) => {
  hoveredCity.value = city;
};

const onLeave = () => {
  hoveredCity.value = '';
};
</script>

<style scoped>
.city-item {
  width: 400px;
  margin: 10px 0;
  padding: 10px;
  border: 1px solid #ccc;
  cursor: pointer;
  background-color: #ffffff; /* Default background color */
  transition: background-color 0.3s ease; /* Smooth transition */
}

.city-item.hovered {
  background-color: #f0f0f0; /* Background color on hover */
}
</style>
