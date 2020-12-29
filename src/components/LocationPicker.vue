

<template>
    <div>
        <h3>Pick a City</h3>
        <!-- Display the city btns -->
        <div v-for="location in locations" :key="location.id" class="btn-container">
            <div class="city-btn" @click="locationUpdate">{{ location.city }}</div>
        </div>
        <!-- inactive class / if city is selecte, active class -->
        <!-- if city is selected, display lat, long  -->
    </div>
</template>

<script>
import weather from 'weather-gov-api'
export default {
  props: [""],
  data() {
    return {
      // pick a city will be an object {cityName : [lat, long] }
      uri: "https://api.weather.gov/points/",
      locations: [
        {
          city: "Miami",
          latLong: [25.761681, -80.191788],
          id: 1,
          selected: false
        },
        {
          city: "Tallahassee",
          latLong: [30.43826, -84.28073],
          id: 2,
          selected: false
        },
        {
          city: "Orlando",
          latLong: [28.538336, -81.379234],
          id: 3,
          selected: false
        }
      ]
      // weather: {
      // contains weather info
      // }
      //
    };
  },
  methods: {
    locationUpdate() {
        // console.log("id", location)
        // weather.getForecast("grid", 25.761681, -80.191788)
        // .then(data => { console.log(data)})
        // .catch(err => console.log(err))
        fetch("https://api.weather.gov/points/25.761681,-80.191788")
        .then( res => res.json())
        .then(data => {
            fetch(data.properties.forecast)
            .then( res => res.json())
            .then(data => {
                console.log(data.properties.periods[0].shortForecast)
            })
        })
        .catch(err => console.log(err.message))
    },

    
    
    // get weather function. Will update the weather object
    // will emit the weather data res
  }
};
</script>

<style>
.btn-container{
    display: flex;
    flex-direction: row;
}

.city-btn {
  cursor: pointer;
  display: block;
  width: 100px;
  margin: 20px auto 0;
  background: #33B4E5;
  color: white;
  padding: 10px;
  border: 0;
  border-radius: 6px;
  font-size: 16px;
}

.city-btn:hover {
    background: #278fb5;
}

.city-btn:active {
    background: #278fb5;
}
</style>
