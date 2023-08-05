<script setup>
  import { ref } from 'vue'
  import DayContainer from './DayContainer.vue'
  import DayNames from './DayNames.vue'
  import MonthName from './MonthName.vue'

  const props = defineProps(['date', 'index', 'max'])

  const [y, m] = props.date.split("-")
  const year = ref(Number(y))
  const month = ref(Number(m))

  const isLeapYear = year => { return (year % 4 == 0 && year % 100 != 0)
                                    || year % 400 == 0 }

  const MONTH = {
     1: { name: "January",   days: 31, key: 1 },
     2: { name: "February",  days: 0,  key: 4 },
     3: { name: "March",     days: 31, key: 4 },
     4: { name: "April",     days: 30, key: 0 },
     5: { name: "May",       days: 31, key: 2 },
     6: { name: "June",      days: 30, key: 5 },
     7: { name: "July",      days: 31, key: 0 },
     8: { name: "August",    days: 31, key: 3 },
     9: { name: "September", days: 30, key: 6 },
    10: { name: "October",   days: 31, key: 1 },
    11: { name: "November",  days: 30, key: 4 },
    12: { name: "December",  days: 31, key: 6 }
  }

  MONTH[2].days = isLeapYear(year.value) ? 29 : 28;


  /* https://www.almanac.com/how-find-day-week */

  const firstDay = (year, month) => {
    if (year < 1753 || year > 2099 || month < 1 || month > 12) return -1;

    const a = year % 100
    const b = a + Math.floor(a / 4)
    let c = b + 1 + MONTH[month].key

    if ((month == 1 || month == 2) && isLeapYear(year)) {
      c -= 1
    }

    if (year > 1752 && year < 1800) {
      c += 4
    } else if (year < 1900) {
      c += 2
    } else if (year >= 2000 && year < 2100) {
      c -= 1
    }

    const d = c % 7

    return d == 0 ? 6 : d - 1
  }
</script>

<template>
  <div>
    <div class="month">
      <MonthName>{{ MONTH[month].name + " " + year }}</MonthName>
      <DayNames />
      <DayContainer :startsOn="firstDay(year, month)" :numberOfDays="MONTH[month].days" />
    </div>
  </div>
  <div v-if="index % 2 == 1 && index != max" class="page-break"></div>
</template>


<style scoped>
.month {
  border: var(--border-style);
  border-top-left-radius: calc(var(--square-side) + var(--border-thickness));
  border-top-right-radius: calc(var(--square-side) + var(--border-thickness));
}

.page-break {
  page-break-after: always;
}
</style>
