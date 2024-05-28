<template>
  <div>
    <CitySelect
        :cities="cityList"
        :selectedCity="selectedCity"
        @update:selectedCity="updateSelectedCity"
    >
      <template #selectedCity>
        <p>Selected City: {{ selectedCity }}</p>
      </template>
    </CitySelect>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import CitySelect from './components/CitySelect.vue';

const cityList = ref([
  'Holmdel, New Jersey',
  'Atlanta, Georgia',
  'San Francisco, California',
  'Basingstoke, United Kingdom',
  'London, Shoreditch, United Kingdom',
  'London, Canary Wharf, United Kingdom',
  'Tel Aviv-Yafo, Israel'
]);

const selectedCity = ref('');

const updateSelectedCity = (city: string) => {
  selectedCity.value = city;
};
</script>
