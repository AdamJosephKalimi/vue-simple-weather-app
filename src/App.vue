<template>
  <div>
    <h1>Simple Weather App</h1>
    <LocationPicker />
    <DisplayWeather />
  </div>

</template>

<script>
import LocationPicker from './components/LocationPicker.vue'
import DisplayWeather from './components/DisplayWeather.vue'


export default {
  name: 'App',
  components: {
    LocationPicker,
    DisplayWeather
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
