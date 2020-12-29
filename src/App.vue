<template>
  <div>
    <h1>Simple Weather App</h1>
    <LocationPicker @weatherData="updateWeather"/>
    <DisplayWeather :weather="weather"/>
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
  },
  data() {
    return {
      weather: {
        temp: null,
        shortForecast: null
      }
    }
  },
  methods: {
    updateWeather(data) {
      console.log("app.vue weather data", data)
      this.weather.temp = data.properties.periods[0].temperature
      this.weather.shortForecast = data.properties.periods[0].shortForecast
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
  color: #2b2b2b;
  margin-top: 30px;
  
}
h1 {
  color: #2b2b2b;
  font-weight: 800;
  letter-spacing: .07ch;
  font-size: 40px;
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
  margin-bottom: 50px;
}
</style>
