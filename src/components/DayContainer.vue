<script setup>
  import { ref } from 'vue'
  import Day from './Day.vue'
  import Tile from './Tile.vue'

  const props = defineProps(["startsOn", "numberOfDays"])

  const offset = Number(props.startsOn)
  const length = Number(props.numberOfDays)

  const days = ref([])
  for (let i = 1; i <= length; i++) days.value.push(i)

  const head = ref(offset)
  const tail = ref(7 - (length + offset) % 7)
</script>

<template>
  <div id="days">
    <div v-if="head">
      <Tile :width=head />
    </div>
    <Day v-for="day in days" :day=day />
    <div v-if="tail && tail < 7">
      <Tile :width=tail />
    </div>
  </div>
</template>

<style>
  #days {
    width: calc(var(--square-side) * 7);

    display: flex;
    flex-wrap: wrap;
  }

</style>
