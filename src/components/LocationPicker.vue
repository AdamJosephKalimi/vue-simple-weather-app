<template>
    <div>
        <h3>PICK LOCATION</h3>
        <!-- Display the city btns -->
        <div class="btn-container">
            <div v-for="location in locations" :key="location.id" @click="locationUpdate(location)" class="city-btn">
                {{ location.city }}
            </div>
        </div>
    </div>
</template>

<script>
import weather from "weather-gov-api";
export default {
  props: [],
  data() {
    return {
      uri: "https://api.weather.gov/points/",
      // Default coords which are updated if user provides location
      selectedCoords: [25.761681, -80.191788],
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
      ],
    };
  },

  mounted() {
    // When app mounts, attempt to get user's location and update it to component data
    let options = {
        enableHighAccuracy: true,
        timeout: 5000,
        maximumAge: 0
    }
    function success(pos) {
        let coords = pos.coords
        if(coords) {
            // Fetch weather for user's current location and update            
            fetch("https://api.weather.gov/points/"+ coords.latitude.toString() + "," + coords.longitude.toString())
            .then(res => res.json())
            .then(data => {
                fetch(data.properties.forecast)
                .then(res => res.json())
                .then(data => {
                let temp = data.properties.periods[0].temperature;
                let shortForecast = data.properties.periods[0].shortForecast;
                this.$emit("weatherData", data);
                })
                .catch(err => console.log(err.message));
            })
            .catch(err => console.log(err.message));

        } else this.latLong = null
    }
    function error(err) {
        console.warn(`ERROR(${err.code}): ${err.message}`);
    }
    navigator.geolocation.getCurrentPosition(success, error, options) 
  },

  methods: {
      
    locationUpdate(city) {
    this.selectedCoords = [ city.latLong[0], city.latLong[1] ]
      
      fetch("https://api.weather.gov/points/"+ city.latLong[0].toString() + "," + city.latLong[1].toString())
        .then(res => res.json())
        .then(data => {
            console.log(data)
          fetch(data.properties.forecast)
            .then(res => res.json())
            .then(data => {
              let temp = data.properties.periods[0].temperature;
              let shortForecast = data.properties.periods[0].shortForecast;
              console.log(data)
              this.$emit("weatherData", data);
            })
            .catch(err => console.log(err.message));
        })
        .catch(err => console.log(err.message));
    },
  }
};
</script>

<style>
.btn-container {
  margin-bottom: 50px;
}

.city-btn {
  cursor: pointer;
  display: block;
  width: 100px;
  margin: 20px auto 0;
  background: #33b4e5;
  color: white;
  padding: 10px;
  border: 0;
  border-radius: 6px;
  font-size: 16px;
  font-weight: 600;
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
}

.city-btn:hover {
  background: #278fb5;
}

.city-btn:active {
  background: #278fb5;
}
</style>
