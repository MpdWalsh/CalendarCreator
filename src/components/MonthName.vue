<script setup>

</script>


<template>
  <div class="monthName">
    <slot />
  </div>
</template>


<style scoped>
.monthName {
  height: calc(1.5 * var(--square-side));
  border: var(--border-style);
  border-top-left-radius: var(--square-side);
  border-top-right-radius: var(--square-side);

  display: flex;
  justify-content: center;
  align-items: center;

  font-family: var(--month-font-family);
  font-size: var(--month-font-size);
}
</style>
