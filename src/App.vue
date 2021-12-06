<template>
  <div id="app">

    <div class="w-full px-40 pb-20">
        <div
            class="flex flex-wrap -mx-2"
            data-cy="leave-calendar"
        >
          <calendar-month
              v-for="(month, index) in months"
              :key="'cal' + month.format('-MM-YYYY')"
              :month="month"
              :month-number="index + 1"
          />
        </div>
    </div>
  </div>
</template>

<script>
import CalendarMonth from "./components/CalendarMonth";
import moment from 'moment-timezone'

export default {
  name: 'App',

  components: {
    CalendarMonth,
  },

  computed: {

    months() {
      let start = moment.utc("2021-01-01")
      const end = moment.utc("2021-12-31")
      let months = []

      while (start.isBefore(end) || start.format('M') === end.format('M')) {
        months.push(start.clone())
        start.add(1, 'month')
      }

      return months
    },

  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
