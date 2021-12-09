<template>
<div>
  <div 
    v-if="arg.event.extendedProps.type == 'blue'" 
    class="flex justify-between items-center px-4 py-1 text-gray-500 relative -top-6 bg-blue-100 border-blue-500 border-2 rounded h-6">
    <span class="text-blue-500 font-bold" :key="date.date()" v-for="date in dates">{{ date.date() }}</span>
  </div>
  <div 
    v-else 
    class="flex justify-between items-center px-4 py-1 text-gray-500 relative -top-6 bg-indigo-100 border-indigo-500 border-2 rounded h-6">
    <span class="text-indigo-500 font-bold" :key="date.date()" v-for="date in dates">{{ date.date() }}</span>
  </div>
</div>
</template>

<script>
import moment from 'moment-timezone'
export default {
  name: "event-component",

  props: {
    arg: {
      type: Object,
      default: () => {},
    },
  },

  data() {
    return {
      dates: []
    }
  },

  mounted() {
    console.log(JSON.stringify(this.arg))
    let start = moment(this.arg.event.start)
    while(moment(start) <= moment(this.arg.event.end)) {
      console.log(start.date())
      this.dates.push(start);
      start = moment(start).add(1, 'days')
    }
  }
}
</script>

<style scoped>

</style>