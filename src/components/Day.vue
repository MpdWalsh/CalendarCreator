<script setup>
  const props = defineProps(['day'])
</script>

<template>
	<div class="day">
		<div class="day-number">
			{{ day }}
		</div>
	</div>
</template>

<style scoped>
.day {
  width: var(--square-side);
  height: var(--square-side);
  border: var(--border-style);

	display: flex;
	justify-content: flex-end;
	align-items: flex-start;
}

.day-number {
	width: calc(var(--square-side) / 4);
	height: calc(var(--square-side) / 4);
	border-left: var(--border-style);
	border-bottom: var(--border-style);

	display: flex;
	justify-content: center;
	align-items: center;

	font-family: var(--day-font-family);
	font-size: var(--day-font-size);
}
</style>
