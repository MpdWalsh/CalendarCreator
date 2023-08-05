<script setup>
  import { ref } from 'vue'
  import Month from './Month.vue'

  const props = defineProps(['from', 'quantity'])

  const dateSequence = ref([])

  const nextMonth = givenMonth => {
    const [y, m] = givenMonth.split("-")
    let year = Number(y)
    let month = Number(m)

    if (month < 12) {
      month += 1
    } else if (month == 12) {
      month = 1
      year += 1
    }

    return year + "-" + (month < 10 ? "0" + month : month)
  }

  let month = props.from
  for (let i = 0; i < Number(props.quantity); i++) {
    dateSequence.value.push(month)
    month = nextMonth(month)
  }

</script>

<template>
  <Month v-for="(date, index) in dateSequence"
    :date="date" :index="index" :max="dateSequence.length - 1" />
</template>

<style scoped>

</style>
