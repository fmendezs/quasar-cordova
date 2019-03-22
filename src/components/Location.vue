<template>
  <div>
    You location is: <strong>{{ location }}</strong>
  </div>
</template>

<script>
export default {
  name: 'location',
  data () {
    return {
      location: 'determining...'
    }
  },
  methods: {
    updateLocation (position) {
      this.location = `Latitude: ${position.coords.latitude}, Longitude: ${position.coords.longitude}`
    },
    onError (error) {
      alert(`code: ${error.code} message: ${error.message}`)
    }
  },
  created () {
    navigator.geolocation.getCurrentPosition(this.updateLocation, this.onError, { enableHighAccuracy: true })
  }
}
</script>

<style lang="stylus">

</style>
