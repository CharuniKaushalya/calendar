<template>
    <div class="sm:w-1/2 lg:w-1/3 xl:w-1/4">
      <div
          class="bg-white border border-2 border-gray-300 overflow-hidden my-leave-calendar"
      >
        <div
            class="pt-1 px-2 text-xl font-bold flex justify-end"
            v-text="month.format('MMM')"
        />
        <calendar
            ref="calendar"
            :events="calendarEvents"
            :config="calendarConfig"
            :selectable="true"
            default-view="dayGridMonth"
            class="leave-calendar"
        />
      </div>
    </div>
</template>

<script>
import '@fullcalendar/core/vdom'
import Calendar from "./Calendar";

export default {
  name: 'CalendarMonth',

  components: {Calendar},

  props: {
      month: {
        type: Object,
        required: true,
      },

      monthNumber: {
        type: Number,
        required: true,
      },
  },

  computed: {
    MothName() {
      return 'Feb'
    },

    calendarEvents() {
      return []
    },

    calendarConfig() {
      return {
        contentHeight: 250,
        eventOverlap: false,
        fixedWeekCount: false,
        showNonCurrentDates: false,
        weekNumberCalculation: 'iso',
        initialDate: "2021-02-01",
        validRange: this.validRange,
        headerToolbar: false,
        eventDisplay: 'block',
      }
    },

    validRange() {
      //moment.utc("2021-02-01")
      let start = this.month
          .clone()
          .startOf('month')
          .format('YYYY-MM-DD')
      let end = this.month
          .clone()
          .endOf('month')
          .add(1, 'day')
          .format('YYYY-MM-DD')

      return { start, end }
    },
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
