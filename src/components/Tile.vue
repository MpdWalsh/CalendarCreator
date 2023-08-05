<script setup>
  const props = defineProps(['width'])
</script>


<template>
	<div class="tile"></div>
</template>


<style scoped>
  .tile {
    width: calc(var(--square-side) * v-bind(props.width));
    height: var(--square-side);
    border: var(--border-style);
  }
</style>
