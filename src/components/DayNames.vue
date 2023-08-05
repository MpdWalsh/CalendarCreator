<script setup>
  import { ref } from 'vue'

  const dayNames = ref(['Su', 'M', 'Tu', 'W', 'Th', 'F', 'Sa'])
</script>


<template>
  <div id="dayHeader">
    <div v-for="day in dayNames" class="dayName">{{ day }}</div>
  </div>
</template>


<style scoped>
#dayHeader {
  display: flex;
}

.dayName {
	width: var(--square-side);
	height: calc(var(--square-side) / 2);
  border: var(--border-style);

	display: flex;
	justify-content: center;
	align-items: center;

  font-family: var(--week-font-family);
  font-size: var(--week-font-size);
}
</style>
