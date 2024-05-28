<template>
  <div>
    <CitySelect
        :cities="cityList"
        :selectedCity="selectedCity"
        @update:selectedCity="updateSelectedCity"
    >
      <template #selectedCity>
        <p>Selected City: {{ selectedCity.name }}</p>
      </template>
    </CitySelect>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import CitySelect from './components/CitySelect.vue';

const cityList = ref([
  { name: 'Holmdel, New Jersey', timezone: 'America/New_York' },
  { name: 'Atlanta, Georgia', timezone: 'America/New_York' },
  { name: 'San Francisco, California', timezone: 'America/Los_Angeles' },
  { name: 'Basingstoke, United Kingdom', timezone: 'Europe/London' },
  { name: 'London, Shoreditch, United Kingdom', timezone: 'Europe/London' },
  { name: 'London, Canary Wharf, United Kingdom', timezone: 'Europe/London' },
  { name: 'Tel Aviv-Yafo, Israel', timezone: 'Asia/Jerusalem' }
]);

const selectedCity = ref({ name: '', timezone: '' });

const updateSelectedCity = (city) => {
  selectedCity.value = city;
};
</script>
