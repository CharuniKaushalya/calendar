<template>
  <FullCalendar
      id="full-calendar"
      ref="fullCalendar"
      :options="calendarOptions"
  >
  <template v-slot:eventContent="arg">
      <event-component
        :arg="arg"
      />
    </template>
 </FullCalendar>
</template>

<script>
import dayGridPlugin from '@fullcalendar/daygrid'
import { defaultsDeep } from 'lodash-es'
import FullCalendar from '@fullcalendar/vue'
import EventComponent from "./event-component";


export default {
  name: "Calendar",

  components: {
    EventComponent,
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
        dayHeaders: false,
        eventTextColor: 'rgba(59, 130, 246, 0.5)',
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