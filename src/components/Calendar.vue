<template>
  <FullCalendar
      id="full-calendar"
      ref="fullCalendar"
      :options="calendarOptions"
  >
 </FullCalendar>
</template>

<script>
import dayGridPlugin from '@fullcalendar/daygrid'
import { defaultsDeep } from 'lodash-es'
import FullCalendar from '@fullcalendar/vue'


export default {
  name: "Calendar",

  components: {
    FullCalendar
  },

  props: {
    events: {
      type: Array,
      default: () => [],
    },

    resources: {
      type: Array,
      default: () => [],
    },

    selectable: {
      type: Boolean,
      default: () => true,
    },

    header: {
      type: [Object, Boolean],
      default: () => false,
    },

    defaultView: {
      type: String,
      required: true,
    },

    config: {
      type: Object,
      default: () => {},
    },

    isResourceAreaHeaderContentEnabled: {
      type: Boolean,
      default: () => false,
    },
  },

  computed: {
    calendarOptions() {
      return defaultsDeep(this.defaultConfig, this.config)
    },

    defaultConfig() {
      return {
        timeZone: 'UTC',
        headerToolbar: this.header,
        events: this.events,
        selectable: this.selectable,
        plugins: [dayGridPlugin],
        initialView: this.defaultView,
        schedulerLicenseKey: 'CC-Attribution-NonCommercial-NoDerivatives',
        resources: this.resources,
        resourceOrder: 'auto',
        select: info => {
          this.$emit('event-created', info)
        },
      }
    },
  },
}
</script>

<style scoped>

</style>