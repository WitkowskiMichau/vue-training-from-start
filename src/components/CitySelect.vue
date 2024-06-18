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
    <p v-if="selectedCity">Current Time: {{ formattedTime }}</p>
    <div v-if="isOpen">Open</div>
    <div v-else>Closed</div>
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

setInterval(() => {
  setLocalTime()
}, 1000);

const getLocalTime = () => {
  return moment().tz(props.selectedCity.timezone)
}
const setLocalTime = () => {
  localTime.value = getLocalTime()
}

const localTime = ref(getLocalTime())

const formattedTime = computed(() => {
  return localTime.value.format('YYYY-MM-DD HH:mm:ss');
});
const isOpen = ref(false);

const handleClick = (city) => {
  emit('update:selectedCity', city);
};

watch(() => props.selectedCity, () => {
  setLocalTime()
}, { immediate: true });

const onHover = (city) => {
  hoveredCity.value = city;
};

const onLeave = () => {
  hoveredCity.value = null;
};

watch(localTime, (newTime) => {
  if (!props.selectedCity.timezone) {
    isOpen.value = false;
    return;
  }

  const currentMoment = moment.tz(newTime, props.selectedCity.timezone);
  const currentHour = currentMoment.hour();

  isOpen.value = currentHour >= 9 && currentHour < 17;
}, { immediate: true });

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
