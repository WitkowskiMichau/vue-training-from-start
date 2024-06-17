<template>
  <div>
    <div
        v-for="city in cities"
        :key="city.name"
        @click="handleClick(city)"
        @mouseenter="onHover(city)"
        @mouseleave="onLeave"
        :class="['city-item', { hovered: city === hoveredCity, selected: city === selectedCity }]"
    >
      {{ city.name }}
    </div>
    <slot name="selectedCity"></slot>
    <p v-if="selectedCity">Current Time: {{ localTime }}</p>
  </div>
</template>

<script setup lang="ts">
import {computed, ref, watch} from 'vue';
import moment from 'moment-timezone';
import { defineProps, defineEmits } from 'vue';

const props = defineProps({
  cities: {
    type: Array,
    required: true
  },
  selectedCity: {
    type: Object,
    required: false,
    default: () => ({ name: '', timezone: '' })
  }
});

const emit = defineEmits(['update:selectedCity']);
const hoveredCity = ref(null);
const localTime = computed(() => {
  if (!props.selectedCity.timezone) return '';
  return moment().tz(props.selectedCity.timezone).format('YYYY-MM-DD HH:mm:ss');
});

const handleClick = (city) => {
  emit('update:selectedCity', city);
};

const onHover = (city) => {
  hoveredCity.value = city;
};

const onLeave = () => {
  hoveredCity.value = null;
};
</script>

<style scoped>
.city-item {
  width: 400px;
  margin: 10px 0;
  padding: 10px;
  border: 1px solid #ccc;
  cursor: pointer;
  transition: background-color 0.3s ease; /* Smooth transition */
}

.city-item.hovered {
  background-color: #f0f0f0; /* Background color on hover */
}

.city-item.selected {
  background-color: #d0d0d0; /* Background color for selected */
}
</style>
