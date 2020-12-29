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
        detailedForecast: null,
        icon: null,
        iconPath: null
      }
    }
  },
  methods: {
    updateWeather(data) {
      console.log("app.vue weather data", data)
      this.weather.icon = data.properties.periods[0].icon
      this.weather.temp = data.properties.periods[0].temperature
      let shortForecast = data.properties.periods[0].shortForecast;
      this.weather.detailedForecast = data.properties.periods[0].detailedForecast

      // Issue with getting assets to render using databinding. Will only render if hardcoded.
      // let key = shortForecast.split('')
      //   for(let i = 0; i <= key.length; i++) {
      //       if(key[i] === ' '){
      //           key[i] = '_'
      //       }
      //   }
      // key = key.join('').toLowerCase()
      // var iconPath ="../assets/" + key + ".svg"
      // this.weather.iconPath = iconPath
      // console.log("App.vue iconpath", iconPath)
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
