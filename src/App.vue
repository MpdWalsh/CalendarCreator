<script setup>
  import { ref, watch } from 'vue'
  import Calendar from './components/Calendar.vue'

  const from = ref('2023-01')
  const quantity = ref('2')
  let calendarKey = ref(0)

  watch(from, () => {
    calendarKey += 1
  })

  watch(quantity, () => {
    calendarKey += 1
  })

</script>

<template>
  <div id="controls">
    <div>
      <label for="month">From:</label>
      <input name="month" type="month"
             min="2000-01" max="2099-1"
             v-model="from">
    </div>
    <div>
      <label for="quantity">How many months:</label>
      <select name="quantity" v-model="quantity">
        <option v-for="m in 12" :value="m">{{ m }}</option>
      </select>
    </div>
  </div>
  <hr>
  <div class="printable-area" >
    <Calendar :key="calendarKey" :from="from" :quantity="quantity" />
  </div>
</template>

<style scoped>
#controls {
  position: absolute;
  top: 20px;
  left: 0;

  width: 100%;

  display: flex;
  justify-content: center;
  gap: 30px;
}

#controls div {
  display: flex;
  gap: 15px;
}

hr {
  position: absolute;
  top: 50px;
  left: 0px;

  width: 100%;
}

#input {
  height: 50px;
}

.printable-area {
  margin-top: 70px;

  display: flex;
  flex-wrap: wrap;
  column-gap: 2.5mm;
  row-gap: 10mm;
  justify-content: center;
  align-items: flex-start;
}

@media print {
  .printable-area {
    visibility: visible;
    margin-top: 10mm;
  }
}
</style>
