<template>
  <div>
    <div
        v-for="city in cities"
        :key="city"
        @click="handleClick(city)"
        @mouseenter="onHover(city)"
        @mouseleave="onLeave"
        :class="['city-item', { hovered: city === hoveredCity, selected: city === selectedCity }]"
    >
      {{ city }}
    </div>
    <slot name="selectedCity"></slot>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import { defineProps, defineEmits } from 'vue';

const props = defineProps({
  cities: {
    type: Array,
    required: true
  },
  selectedCity: {
    type: String,
    required: false,
    default: ''
  }
});

const emit = defineEmits(['update:selectedCity']);
const hoveredCity = ref('');

const handleClick = (city: string) => {
  emit('update:selectedCity', city);
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
  transition: background-color 0.3s ease; /* Smooth transition */
}

.city-item.hovered {
  background-color: #f0f0f0; /* Background color on hover */
}

.city-item.selected {
  background-color: #d0d0d0; /* Background color for selected */
}
</style>
