<template>
  <q-page>
    <div class="q-pa-md select self-center">
      <div class="q-gutter-md">
        <q-select filled v-model="zone" :options="options" />
      </div>
    </div>
    <div class="clock">
      <p class="date">{{currentDate}}</p>
      <p class="time">{{currentTime}}</p>
    </div>
  </q-page>
</template>

<script>
import { date } from 'quasar'
let now = new Date()

export default {
  name: 'PageDate',
  data () {
    return {
      currentDate: date.formatDate(now, 'MMM, Do YYYY'),
      currentTime: date.formatDate(now, 'HH:mm:ss'),
      intervalTime: this.updateTime(),
      options: [{ label: 'Local Time', value: 0 }, { label: 'New York', value: -5 }, { label: 'Fiji', value: 12 }, { label: 'Moscow', value: 3 }],
      zone: null
    }
  },
  methods: {
    updateTime () {
      this.interval = setInterval(() => {
        now = new Date()
        if (this.zone !== null && this.zone.value !== 0) {
          var utc = now.setTime(now.getTime() + now.getTimezoneOffset() * 60 * 1000)
          now = new Date(utc + (3600000 * this.zone.value))
        }
        this.currentDate = date.formatDate(now, 'MMM, Do YYYY')
        this.currentTime = date.formatDate(now, 'HH:mm:ss')
      }, 1000)
    }
  }
}
</script>

<style lang="stylus">
  .clock
    font-family 'Share Tech Mono', monospace
    color #0f0f0f
    text-align center
    color #0f0f0f
    text-shadow 0 0 20px rgba(15, 15, 15, 1),  0 0 20px rgba(15, 15, 15, 0)
  .time
    letter-spacing 0.05em
    font-size 60px
    padding 5px 0
  .date
    letter-spacing 0.1em
    font-size 24px
  .select
    margin-left 25%
    max-width 50%
    min-width 200px
</style>
